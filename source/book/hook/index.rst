Hook
====

Menu
----

To overwrite the menu list you can use the ``enhavo_admin.menu`` hook.

.. code-block:: php

    function onMenu($menuEvent)
    {
        $menu = $menuEvent->getMenu()
        $menu->add();
        $menu->delete();
        $menu->disable();
    }
