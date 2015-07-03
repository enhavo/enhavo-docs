Menu
====

The main menu in the admin is configurable over the ``enhavo_admin.menu``.
You don't need to add the logout button. It will be added automatically.

.. code-block:: yaml

    enhavo_admin:
        menu:
            user:
                label: label.user
                route: enhavo_user_user_index
                role: ROLE_ESPERANTO_USER_USER_INDEX
            group:
                label: label.group
                route: enhavo_user_group_index
                role: ROLE_ESPERANTO_USER_GROUP_INDEX

Hook
----

You can hook the menu with the event ``enhavo_admin.menu`` before it
will be rendered.

Note, that by default there is already a hook, which is
responsible for the logout button, permissions and style. If you
want to be sure to hook after the default hook, you need to
increase your order number.

.. code-block:: php

    namespace enhavo\ProjectBundle\EventListener;

    use enhavo\AdminBundle\Menu\MenuEvent;

    class MenuEventListener
    {
        public function onMenu(MenuEvent $event)
        {
            $menu = $event->getMenu();
            foreach($menu->getChildren() as $child) {
                $menu->setAttribute('class', 'menu');
            }
        }
    }

.. code-block:: yaml

    enhavo_project.menu_event_listener:
        class: enhavo\ProjectBundle\EventListener\MenuEventListener
        tags:
          - { name: kernel.event_listener, event: enhavo_admin.menu, method: onMenu  }

