Index Route
============

.. code-block:: yaml

    esperanto_app_index:
        path: /admin/esperanto/app/resource/index
        methods: [GET]
            defaults:
                _controller: app.controller.user:showAction
                _sylius:
                    template: App:Backend/User:show.html.twig
                _admin
                    view:
                        viewer: viewer.index
                        parameters:
                            param1: value1
                            param2: value2
                    stylesheets:
                        esperanto_app_style:
                            resource: '@esperantoAppBundle/Resource/public/css/style.css'
                            depends: ~
                    javascripts:
                        esperanto_app_bootstrap:
                            resource: '@esperantoAppBundle/Resource/public/js/bootstrap.css'
                            depends: jquery