Create Route
============

.. code-block:: yaml

    esperanto_page_page_create:
        path: /admin/esperanto/page/page/create
        methods: [GET,POST]
        options:
            expose: true
        defaults:
            _controller: esperanto_page.controller.page:createAction
            _sylius:
                template: esperantoAdminBundle:Resource:create.html.twig
            _viewer:
                type: create
                parameters:
                    param1: value1
                    param2: value2
                tabs:
                    page:
                        label: page
                        template: esperantoPageBundle:Tab:page.html.twig
                    content:
                        label: Content
                        template: esperantoPageBundle:Tab:content.html.twig
                    seo:
                        label: Seo
                        template: esperantoPageBundle:Tab:seo.html.twig
                buttons:
                    cancel:
                        route:
                        display: true
                        role: ~
                        label: label.cancel
                        icon: close
                    save:
                        route: ~
                        display: true
                        role: ~
                        label: label.save
                        icon: check
                    preview:
                        route: esperanto_page_page_preview
                        display: true
                        role: ~
                        label: label.preview
                        icon: eye
                form:
                    template: esperantoAdminBundle:View:tab.html.twig
                    theme: ~
                    action: esperanto_page_page_create