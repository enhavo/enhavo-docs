Table Route
============

.. code-block:: yaml

    esperanto_app_table:
        path: /admin/esperanto/app/resource/index
        methods: [GET]
            defaults:
                _controller: app.controller.user:createAction
                _sylius:
                    template: App:Backend/User:show.html.twig
                    criteria:
                        username: $username
                        enabled:  true
                    repository:
                        method: findOneWithFriends
                        arguments: [$username]
                    sortable: true
                    sorting:
                        score: desc
                    paginate: 5
                    limit: 3
                _viewer
                    type: table
                    parameters:
                        param1: value1
                        param2: value2
                    table:
                        width: 5
                        columns:
                            id:
                                title: ID
                                field: id
                                width: 1
                            title:
                                title: ID
                                field: id
                                width: 1
                            public:
                                label: public
                                property: public
                                widget: esperantoAdminBundle:Widget:boolean.html.twig