Index Route
============

The index extends from the standard app route, but is bind to resource. The advantage is, that we only need
a short route definition, but it is as extendable as the app route.

Here you can see the minimum route definition:

.. code-block:: yaml

    enhavo_app_resource_index:
        path: /enhavo/app/resource/index
        methods: [GET]
        defaults:
            _controller: enhavo_reference.controller.reference:indexAction
            _sylius:
                template: enhavoAdminBundle:Resource:index.html.twig

This is really short, isn't it? Here you can see the full standard definition, which is made
automatically by the viewer and controller.

.. code-block:: yaml

    enhavo_app_resource_index:
        path: /enhavo/app/resource/index
        methods: [GET]
        defaults:
            _controller: enhavo_app.controller.resource:indexAction
            _sylius:
                template: enhavoAdminBundle:Resource:index.html.twig
            _viewer:
                type: index
                blocks:
                    table:
                        type: enhavo_page_page_table
                        parameters:
                            table_route: enhavo_page_page_table
                            update_route: enhavo_page_page_update
                actions:
                    create:
                        type: overlay
                        route: enhavo_page_page_create
                        icon: plus
                        label: label.create




