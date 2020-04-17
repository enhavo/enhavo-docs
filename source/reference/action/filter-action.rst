Filter Action
=============

Opens an additional view that contains all available filters of a table.

.. csv-table::
    :widths: 50 150

    Type , filter
    Options , "- | :ref:`label <label_filter>`
    - | :ref:`icon <icon_filter>`
    - | :ref:`translation_domain <translation_domain_filter>`
    - | :ref:`permission <permission_filter>`
    - | :ref:`hidden <hidden_filter>`"
    Class, :class:`Enhavo\\Bundle\\AppBundle\\Action\\Type\\FilterActionType`
    Parent, `Enhavo\\Bundle\\AppBundle\\Action\\AbstractActionType`


Basic Usage
-----------

Filters must be added under "my_entity_table". By default, this action is only available for the index window which is
represented by the "my_entity_index" route. How to create or add custom filters is described :ref:`here <add_custom_filter>`
in more detail.

.. code-block:: yaml

    app_entity_index:
        options:
            expose: true
        path: /app/entity/index
        methods: [GET]
        defaults:
            _controller: app.controller.entity:indexAction
            _sylius:
                viewer:
                    actions:
                        filter:
                            type: filter

    app_entity_table:
        options:
            expose: true
        path: /app/entity/table
        methods: [GET,POST]
        defaults:
            _controller: app.controller.entity:tableAction
            _sylius:
                filters:
                    my_filter:
                        type: property_type
                        property: property

Options
-------

.. _label_filter:
.. |default_label| replace:: `label.filter`
.. include:: /reference/action/option/label.rst

.. _icon_filter:
.. |default_icon| replace:: `filter_list`
.. include:: /reference/action/option/icon.rst

.. _translation_domain_filter:
.. |default_translationDomain| replace:: `EnhavoAppBundle`
.. include:: /reference/action/option/translationDomain.rst

.. _permission_filter:
.. |default_permission| replace:: null
.. include:: /reference/action/option/permission.rst

.. _hidden_filter:
.. |default_hidden| replace:: `false`
.. include:: /reference/action/option/hidden.rst



