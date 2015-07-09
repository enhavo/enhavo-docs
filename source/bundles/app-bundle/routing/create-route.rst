Create Route
============

.. code-block:: yaml

    enhavo_page_page_create:
        path: /admin/enhavo/page/page/create
        methods: [GET,POST]
        options:
            expose: true
        defaults:
            _controller: enhavo_page.controller.page:createAction
            _sylius:
                template: enhavoAdminBundle:Resource:create.html.twig
            _viewer:
                type: create
                parameters:
                    param1: value1
                    param2: value2
                tabs:
                    page:
                        label: page
                        template: enhavoPageBundle:Tab:page.html.twig
                    content:
                        label: Content
                        template: enhavoPageBundle:Tab:content.html.twig
                    seo:
                        label: Seo
                        template: enhavoPageBundle:Tab:seo.html.twig
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
                        route: enhavo_page_page_preview
                        display: true
                        role: ~
                        label: label.preview
                        icon: eye
                form:
                    template: enhavoAdminBundle:View:tab.html.twig
                    theme: ~
                    action: enhavo_page_page_create