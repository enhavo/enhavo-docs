Configuration
=============

.. code-block:: yaml

    esperanto_admin:
        permission_check: false
        stylesheets:
            esperanto_app_style:
                resource: '@esperantoAppBundle/Resource/public/css/style.css'
                depends: ~
        javascripts:
            esperanto_app_bootstrap:
                resource: '@esperantoAppBundle/Resource/public/js/bootstrap.css'
                depends: jquery
        menu:
            homepage:
                title: Homepage
                route: esperanto_homepage
                role: HOMEPAGE_ROLE
            download:
                title: Download
                route: esperanto_download_index
                role: DOWNLOAD_ROLE