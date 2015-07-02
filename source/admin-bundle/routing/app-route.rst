App Route
=========

Before you use the app route, you should know what we understand under ``actions`` and ``blocks``.
The app route is responsible to display these to kinds of abstraction. It is fully independent on any
data model. On this Picture you can see how the app route could render them.

.. image:: ../../_drawio/admin-wireframe.png


Actions
-------

Actions are something like buttons. If you click on these buttons, there will be executed something.
Normally just an overlay will be displayed. The overlay will provide a form, where the user can change
data.

Blocks
------

A block is small unit with its own logic. It could also provide some clickable events. But the focus is
to presented some information.

Route
-----

Here is an example route

.. code-block:: yaml

    esperanto_app_index:
        path: /esperanto/app/index
        methods: [GET]
        defaults:
            _controller: esperanto_admin.controller.resource:indexAction
            _sylius:
                template: esperantoAppBundle:App:index.html.twig
            _viewer:
                type: app
                parameters:
                    name: value
                blocks:
                    table:
                        type: esperanto_page_page_table
                        parameters:
                            table_route: esperanto_page_page_table
                            update_route: esperanto_page_page_update
                actions:
                    create:
                        type: overlay
                        route: esperanto_page_page_create
                        icon: plus
                        label: label.create
