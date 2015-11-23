Update Route
============

.. code-block:: yaml

    enhavo_page_page_update:
        options:
            expose: true
        path: /admin/enhavo/page/page/update/{id}
        methods: [GET,POST]
        defaults:
            _controller: enhavo_page.controller.page:updateAction
            _sylius:
                template: enhavoAdminBundle:Resource:update.html.twig
            _viewer:
                type: edit
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
                    delete:
                        route:
                        display: true
                        role: ~
                        label: label.delete
                        icon: trash
                form:
                    template: enhavoAdminBundle:View:tab.html.twig
                    theme: ~
                    action: enhavo_page_page_update
                    delete: enhavo_page_page_delete