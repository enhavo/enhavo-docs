Dynamic routing
===============

It is also possible to use dynamic routing for the entities.
For the implementation we use the ``SymfonyCMF RoutingBundle``.
Usually dynamic routing is used in the frontend to have a nice seo url.
This following example will show you how to add a url field
to your entity and how you map it to a controller action.

Relation
--------

First we need to tell our application that an entity has a ``manyToOne`` relation
to a route. We use yaml for the meta data.

.. code-block:: yaml

    manyToOne:
        route:
            cascade: ['persist', 'refresh', 'remove']
            targetEntity: esperanto\AdminBundle\Entity\Route

.. note::

    The relation between the entity and route should be ``oneToOne``,
    but we have some problems with the owning entity in this case,
    so it is better to use the ``manyToOne`` relation, so the owning side
    is clear.

Here is the php source for the meta data.

.. code-block:: php

    <?php

    /**
     * @var \esperanto\AdminBundle\Entity\Route
     */
    private $route;

    /**
     * @return \esperanto\AdminBundle\Entity\Route
     */
    public function getRoute()
    {
        return $this->route;
    }

    /**
     * @param \esperanto\AdminBundle\Entity\Route $route
     */
    public function setRoute($route)
    {
        $this->route = $route;
    }


Service
-------

Did you wonder why we don`t add relation informations on the route side?
This is because we have a dynamic relation. The content of a route
could be any entity. So this is we just save some type information.
And if a route wants to have his content, we load it on demand.
For this we need to tell to application some mapping informations.
These will be done by a service.

An entity should be configurable by the ``SymfonyCMF RoutingBundle``. If it is
we have a some parameters and services, added by sylius.
So that we can configure it one place, we just pass the parameters
to our service.

.. code-block:: yaml

    parameters:
        esperanto_page.page.route_content_loader.class: esperanto\AdminBundle\Route\RouteContentLoader

    services:
        esperanto_page.page.route_content_loader:
            class: %esperanto_page.page.route_content_loader.class%
            arguments:
                - 'esperanto_page.page'
                - %esperanto_page.model.page.class%
                - 'esperanto_page.repository.page'
            tags:
                - { name: esperanto_route_content_loader }

.. note::

    The third argument is the name of the service, but not the service directly.
    The ``@`` here is missing, because we need some lazy load for getting the service.
    If we don`t do this, we have some loops in our dependencies.

Form
----

To add an url field in our form we just use this simple snippet.
There is already a form type ``esperanto_route``, which handle
all we need. Also the contraints, so we use a clean and unique url.

.. code-block:: php

    <?php

    $builder->add('route', 'esperanto_route');

If you render your form manually, you shouln't forget to add it in your template file.

.. code-block:: twig

    {{ form_row(form.route) }}

Controller
----------

And last but not least, we have to define our controller, and add some
mapping information to the ``SymfonyCMF RoutingBundle``. The mapping contains
the class name of our entity and the action which should be called for it.

.. code-block:: yaml

    cmf_routing:
        dynamic:
            controllers_by_class:
                esperanto\ProjectBundle\Entity\Page: esperantoProjectBundle:Main:page

In our yaml we use ``esperantoProjectBundle:Main:page`` as action, so we also have to add this to
our Controller.

.. code-block:: php

    <?php

    public function pageAction(Page $contentDocument)
    {
        return $this->render('esperantoProjectBundle:Page:page.html.twig', array(
            'page' => $contentDocument
        ));
    }

.. note::

    The first parameter name for the action must be named ``$contentDocument``.
    Otherwise you will get some errors.