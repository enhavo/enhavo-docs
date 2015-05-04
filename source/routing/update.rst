Update Route
============

.. code-block:: yaml

    esperanto_app_update:
        path: /admin/esperanto/app/resource/index
        methods: [GET]
            defaults:
                _controller: app.controller.user:updateAction
                _sylius:
                    template: App:Backend/User:show.html.twig
                    repository:
                        method: findOneWithFriends
                        arguments: [$username]
                _admin
                    view:
                        viewer: viewer.create.tab
                        parameters:
                            param1: value1
                            param2: value2
                        tabs:
                            content:
                                title: Content
                                template: esperantoAppBundle:Admin/Tabs:content.html.twig
                            seo:
                                title: Seo
                                template: esperantoAppBundle:Admin/Tabs:seo.html.twig
                        preview:
                            route: esperanto_app_show
                            parameter:
                                - id