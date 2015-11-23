AppBundle
==========

.. code-block:: yaml

    enhavo_admin:
        permission_check: false
        stylesheets:
            enhavo_app_style:
                resource: '@enhavoAppBundle/Resource/public/css/style.css'
                depends: ~
        javascripts:
            enhavo_app_bootstrap:
                resource: '@enhavoAppBundle/Resource/public/js/bootstrap.css'
                depends: jquery
        menu:
            homepage:
                title: Homepage
                route: enhavo_homepage
                role: HOMEPAGE_ROLE
            download:
                title: Download
                route: enhavo_download_index
                role: DOWNLOAD_ROLE