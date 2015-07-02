Delete Route
============

.. code-block:: yaml

    esperanto_page_page_delete:
        path: /admin/esperanto/page/page/delete/{id}
        defaults:
            _controller: esperanto_page.controller.page:deleteAction