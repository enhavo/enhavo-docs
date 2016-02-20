Sorting Routes
==============

A resource might be sortable, meaning it has an order which can be changed by the user. In this case, it needs two
additional routes for the events of moving the object up and down.

+-------------------------------+-------------------------------------------------------------------------+
| **Parameters**                | Description                                                             |
+-------------------------------+-------------------------------------------------------------------------+
| **_sylius.sortable_position** | Property of that model or row (int) which is used for sorting           |
+-------------------------------+-------------------------------------------------------------------------+
| **_viewer.sorting**           | **desc** (default) means higher values come before lower values, with 0 |
|                               | being the last element; **asc** is the other way around                 |
+-------------------------------+-------------------------------------------------------------------------+


.. code-block:: yaml

    enhavo_page_page_move_up:
        options:
            expose: true
        path: /admin/enhavo/page/page/move-up
        methods: [POST]
        defaults:
            _controller: enhavo_page.controller.page:moveUpAction
            _sylius:
                sortable_position: position
            _viewer:
                sorting: desc


.. code-block:: yaml

    enhavo_page_page_move_down:
        options:
            expose: true
        path: /admin/enhavo/page/page/move-down
        methods: [POST]
        defaults:
            _controller: enhavo_page.controller.page:moveDownAction
            _sylius:
                sortable_position: position
            _viewer:
                sorting: desc

