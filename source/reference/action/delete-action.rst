Delete Action
=============

Deletes the current resource and closes the window.

.. csv-table::
    :widths: 50 150

    Type , delete
    Require , "- | :ref:`route <route_delete>`"
    Options ,"- | :ref:`label <label_delete>`
    - | :ref:`translation_domain <translation_domain_delete>`
    - | :ref:`icon <icon_delete>`
    - | :ref:`permission <permission_delete>`
    - | :ref:`hidden <hidden_delete>`
    - | :ref:`confirm <confirm_delete>`
    - | :ref:`confirm_message <confirm_message_delete>`
    - | :ref:`confirm_label_ok <confirm_label_ok_delete>`
    - | :ref:`confirm_label_cancel <confirm_label_cancel_delete>`
    - | :ref:`route_parameters <route_parameters_delete>`"
    Class, :class:`Enhavo\\Bundle\\AppBundle\\Action\\Type\\DeleteActionType`
    Parent, `Enhavo\\Bundle\\AppBundle\\Action\\AbstractUrlActionType`


Require
-------

.. _route_delete:

route
~~~~~

**type**: `string`
**default**: `null`

Define which route should be used to delete the selected resource.

.. code-block:: yaml

    actions:
        delete:
            type: delete
            route: my_delete_route

Options
-------

.. _label_delete:
.. |default_label| replace:: `label.delete`
.. include:: /reference/action/option/label.rst

.. _translation_domain_delete:
.. |default_translationDomain| replace:: `EnhavoAppBundle`
.. include:: /reference/action/option/translationDomain.rst

.. _icon_delete:
.. |default_icon| replace:: `delete`
.. include:: /reference/action/option/icon.rst

.. _permission_delete:
.. |default_permission| replace:: null
.. include:: /reference/action/option/permission.rst

.. _hidden_delete:
.. |default_hidden| replace:: `false`
.. include:: /reference/action/option/hidden.rst

.. _confirm_delete:
.. |default_confirm| replace:: `true`
.. include:: /reference/action/option/confirm.rst

.. _confirm_message_delete:
.. |default_confirm_message| replace:: `message.delete.confirm`
.. include:: /reference/action/option/confirm_message.rst

.. _confirm_label_ok_delete:
.. |default_confirm_label_ok| replace:: `label.ok`
.. include:: /reference/action/option/confirm_label_ok.rst

.. _confirm_label_cancel_delete:
.. |default_confirm_label_cancel| replace:: `label.cancel`
.. include:: /reference/action/option/confirm_label_cancel.rst

.. _route_parameters_delete:
.. |default_route_parameters| replace:: []
.. include:: /reference/action/option/routeParameters.rst