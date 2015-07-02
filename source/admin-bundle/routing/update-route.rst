Update Route
============

.. code-block:: yaml

    esperanto_page_page_update:
        options:
            expose: true
        path: /admin/esperanto/page/page/update/{id}
        methods: [GET,POST]
        defaults:
            _controller: esperanto_page.controller.page:updateAction
            _sylius:
                template: esperantoAdminBundle:Resource:update.html.twig
            _viewer:
                type: edit
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
                    delete:
                        route:
                        display: true
                        role: ~
                        label: label.delete
                        icon: trash
                form:
                    template: esperantoAdminBundle:View:tab.html.twig
                    theme: ~
                    action: esperanto_page_page_update
                    delete: esperanto_page_page_delete