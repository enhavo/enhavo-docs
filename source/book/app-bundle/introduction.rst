Introduction
============

What is the AppBundle?
----------------------

The AppBundle provide a handful of useful functions and workflows, which helps you
to handle the input and output of any model. The AppBundle depends not on a concrete
model. For this bundle a model is a very abstract thing, which needs to put somewhere
and receive it there again for updating.
In a normal web application, we expect to have something like a MVC architecture.
Therefor we would write our Model, Controller and our View. If we do it the symfony way
right, we write also a form type and finally we add the routing for our controller.
With this Bundle, there is no need for writing controller and views.

What we do now, is to write our concrete model. With doctrine, these is a very basic thing.
If we have written our form type too. We just need to registers them in the config and add the routing.
The big magic here is all in the route. The route provides configuration which make it possible to decide
a lot of things for the controller and for the view.

So what this bundle do, is just give you some standard practise ways to handle your model in our controller
and view. And if you have some requirements, which our bundle doesn't provide, we have an good api to add these
requirements easily.

A very standard way to handle your data
---------------------------------------

Ok, lets do some simple examples to see what the benefits are for your application.
Imagine a library, where we have just books. First, we would add our model.

.. code-block:: php

    <?php

        namespace Acme\LibraryBundle\Model\Book

        class Book {
            private $author;
            private $title;
            function setAuthor() { /* you know what here is to do */ }
            //setters, getters
        }

If we have a model, we also need the FormType

.. code-block:: php

    <?php

        namespace Acme\LibraryBundle\Form\Type

        class BookType extends AbstractType {
            public function builder //..
        }


Now, you add your controller. Of course our controller need the basic CRUD functions.

.. code-block:: php

    <?php

        namespace Acme\LibraryBundle\Controller

        class BookController extends Controller {
            public function createAction() {  /* you know what here is to do */ }
            public function readAction() {  /* you know what here is to do */ }
            public function updateAction() {  /* you know what here is to do */ }
            public function deleteAction() {  /* you know what here is to do */ }
        }

After this we write the views.

.. code-block:: twig

    {% block create %}
        {{ form }}
    {% endblock %}

    {% block read %}
        {{ form }}
    {% endblock %}

    {% block update %}
        {{ form }}
    {% endblock %}

    {% block delete %}
        {{ form }}
    {% endblock %}

And last but not least, we add the routing.

.. code-block:: yaml

    acme_library_create:
        path: /acme/library/create
        methods: [GET]
        defaults:
            _controller: AcmeLibraryBundle:Book:create

    acme_library_read:
        path: /acme/library/read
        methods: [GET]
        defaults:
            _controller: AcmeLibraryBundle:Book:read

    acme_library_update:
        path: /acme/library/update
        methods: [GET]
        defaults:
            _controller: AcmeLibraryBundle:Book:update

    acme_library_delete:
        path: /acme/library/delete
        methods: [GET]
        defaults:
            _controller: AcmeLibraryBundle:Book:delete

After this we can add and receive the book model. As a developer, it should be easy for you.
It's a common way, and if we have a hole bunch of models, this will be a hard copy and paste work.
So this is where the AppBundle wants to help. Reduce code and define a standard workflow to CRUD your data.
This will reduce your code and make your view clean.

How we do this shorter
----------------------

The question is, where can we add a standard workflow to reduce duplicated code, without losing flexibility.
The answer is, in the controller and the view. So what we do is just leave the part of the view and controller.
Instead we add our model to the configuration file and update our routes.

.. code-block:: yaml

    //config file

.. code-block:: yaml

    //routing
    acme_library_create:
        path: /acme/library/create
        methods: [GET]
        defaults:
            _controller: AcmeLibraryBundle:Book:create

    acme_library_read:
        path: /acme/library/read
        methods: [GET]
        defaults:
            _controller: AcmeLibraryBundle:Book:read

    acme_library_update:
        path: /acme/library/update
        methods: [GET]
        defaults:
            _controller: AcmeLibraryBundle:Book:update

    acme_library_delete:
        path: /acme/library/delete
        methods: [GET]
        defaults:
            _controller: AcmeLibraryBundle:Book:delete

Maybe you ask yourself, why we can't we add the routing dynamically, cause this is
als a copy and paste work too? Yes, that's correct. But in the routing we want to add our flexibility.
There're some bundles, like the SonataAdminBundle, which add the routing also.
But for example, if we don't want a delete route? Or we just want to use a different template or form?
Then we have to do some have work and extend the controller and overwrite some functions.
This is what we don't want to do. We want to configure all of these things, and we want to do it
on a very natured place. And in our opinion, this is the route. So for example, if we want to
change the form template, we just pass this information to the route definition.

.. code-block:: yaml

    //routing
    acme_library_create:
        path: /acme/library/create
        methods: [GET]
        defaults:
            _controller: AcmeLibraryBundle:Book:create
            _viewer:
                form:
                    template: AcmeLibraryBundle:Book:form.html.twig

Of course the route provide much more features and options. This should only give you
an idea what this bundle wants to do and where it can help you doing your work well down.
The next chapters will give you a deeper understanding what you can do.


How does it work
----------------

At the beginning we told you the concept of the AppBundle. Now we will go a little bit deeper and
clean up with some wording.

The Viewer
----------


