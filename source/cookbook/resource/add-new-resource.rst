Add new resource
================

You can easily add a new resource to the CMS by following these steps:

1) Add resource to menu
2) Generate new routes
3) Create a controller
4) Add configuration
5) Create an Entity and FormType

As an example, we will be adding a resource called project.

Add resource to menu
--------------------

First we add the new resource to the menu in ``app/config/enhavo.yml``

.. code-block:: yml

    menu:
        project:
            label: label.project
            route: acme_project_project_index
            role: ROLE_ESPERANTO_PROJECT_PROJECT_INDEX

Generate new routes
-------------------

Now generate all the routes you need for the new resource.

.. code-block:: bash

    app/console enhavo:generate:routing acme_project project

If you want your resource to be sortable by the user, you can use the optional parameter "sorting" to additionally
generate sorting behaviour. The value of the parameter is a property type integer in your resource entity to save the
items position. In this example it is called ``order``.

.. code-block:: bash

    app/console enhavo:generate:routing acme_project project --sorting="order"

Create a new file called ``project.yml`` in ``ProjectBundle/Resources/config/routing``.
Copy the routes from the terminal into it.

After you have done this, you have to tell the ``routing.yml`` in ``app/config`` where to find your new ``project.yml``

.. code-block:: yml

    acme_project_project:
        resource: "@acmeProjectBundle/Resources/config/routing/project.yml"
        prefix:   /

Create a controller
-------------------

Add a new controller ``ProjectController`` for the resource in ``ProjectBundle/Controller``.
The new controller extends the ``ResourceController`` from ``Enhavo\Bundle\AppBundle\Controller``

.. code-block:: php

    <?php

    use Enhavo\Bundle\AppBundle\Controller\ResourceController;

    class ProjectController extends ResourceController
    {

    }

Add configuration
-----------------

Now you need to add the new resource to the configuration.
You can do this in two different ways.

Either you can do it in the ``config.yml`` in ``app/config``:

.. code-block:: yml

    sylius_resource:
        resources:
            acme_project.project:
                driver: doctrine/orm
                object_manager: default
                templates: acme_project:Project
                classes:
                    model: acme\ProjectBundle\Entity\Project
                    controller: acme\ProjectBundle\Controller\ProjectController

or you add the resource to the ``Configuration.php`` in ``ProjectBundle/DependencyInjection``:

.. code-block:: php

    <?php
    // The resources
            ->children()
                ->arrayNode('classes')
                ->addDefaultsIfNotSet()
                    ->children()
                        ->arrayNode('project')
                        ->addDefaultsIfNotSet()
                            ->children()
                                ->scalarNode('model')->defaultValue('acme\ProjectBundle\Entity\Project')->end()
                                ->scalarNode('controller')->defaultValue('acme\ProjectBundle\Controller\ProjectController')->end()
                                ->scalarNode('repository')->end()
                                ->scalarNode('form')->defaultValue('acme\ProjectBundle\Form\Type\ProjectType')->end()
                                ->scalarNode('admin')->defaultValue('Enhavo\Bundle\AppBundle\Admin\BaseAdmin')->end()
                            ->end()
                        ->end()
                    ->end()
                ->end()
            ->end()
        ;

If you use the second option, the file ``ProjectBundle/DependencyInjection\AcmeProjectExtenstion.php`` has to extend
``SyliusResourceExtension``, otherwise the services won't work.

Create an Entity and FormType
-----------------------------

Finally you can create the Entity and FormType.

Create the Entity with the following command.

.. code-block:: bash

    app/console doctrine:generate:entity

After that you have to update your database.

.. code-block:: bash

    app/console doctrine:schema:update --force

For the FormType add a new file called ``ProjectType.php`` to ``ProjectBundle/Form/Type``.

.. code-block:: php

    <?php

    namespace acme\ProjectBundle\Form\Type;

    use Symfony\Component\Form\FormBuilderInterface;
    use Symfony\Component\OptionsResolver\OptionsResolverInterface;
    use Symfony\Component\Form\AbstractType;

    class ProjectType extends AbstractType
    {
        public function buildForm(FormBuilderInterface $builder, array $options)
        {
            //Here you add the fields you have just added to the entity
            //In our case for example 'title' and 'text'
            $builder->add('title', 'text', array(
                'label' => 'label.title'
            ));
            $builder->add('text', 'wysiwyg', array(
                'label' => 'label.text'
            ));
        }

        public function setDefaultOptions(OptionsResolverInterface $resolver)
        {
            $resolver->setDefaults(array(
                'data_class' => 'acme\ProjectBundle\Entity\Project'
            ));
        }

        public function getName()
        {
            return 'acme_project_project';
        }
    }

To use the form you have to add the service in the ``service.yml`` on your own.

.. code-block:: yml

    services:
        acme_project_project:
            class: %acme_project.form.type.project.class%
            tags:
                - { name: form.type }


