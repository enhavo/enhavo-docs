Table Route
============


Viewer
------

+----------------+----------------------------------------------------------------------------------+
| **parameters** | List of parameters pass to the twig template                                     |
+----------------+----------------------------------------------------------------------------------+
| **table**      | Configuration for the specific table                                             |
+----------------+----------------------------------------------------------------------------------+

Table
-----

.. code-block:: yaml

    table:
        width: 5
        columns:
            id:
                title: ID
                property: id
                width: 1
            title:
                title: ID
                property: id
                width: 1
            public:
                label: public
                property: public
                widget: EnhavoAdminBundle:Widget:boolean.html.twig


+----------------+----------------------------------------------------------------------------------+
| **title**      | The header of this column                                                        |
+----------------+----------------------------------------------------------------------------------+
| **property**   | Property of that model or row, which should be use to display                    |
+----------------+----------------------------------------------------------------------------------+
| **widget**     | A template file, that render that table cell                                     |
+----------------+----------------------------------------------------------------------------------+
| **width**      | Define the width of the column                                                   |
+----------------+----------------------------------------------------------------------------------+

Width
-----

You can define a width for the the table itself and per column. How wide it's in the end, is up to the
both vars in dependency. The wide of a table is every time the same, cause it is responsive and uses
the bootstrap grid, which has 12 columns by default. So if you define the table with 8 and a two columns with
4 it will map the quotient to the 12 column grid. In this case bot column have 50% of the full table so it uses
6 column spaces.

Widget
------

A Widget helps you to display a table cell to your specific needs.

Here is an example how a widget file can look like. The value of the property will pass the widget file
as ``value``. You can now define how it should be rendered.

.. code-block:: twig

    {# EnhavoAdminBundle:Widget:date.html.twig #}
    {% if value %}
        {{ value.format('d.m.Y') }}
    {% endif %}

Route
-----

Here is a full configuration example of a table route

.. code-block:: yaml

    enhavo_app_table:
        path: /admin/enhavo/app/resource/index
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
                                widget: enhavoAdminBundle:Widget:boolean.html.twig