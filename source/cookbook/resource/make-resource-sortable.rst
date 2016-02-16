Making a resource sortable
==========================

Sometimes the instances of your resource need to be in a specific order that can be changed by the user. An example
would be the entries of a menu, or slides in a slider.

For this example, we will use the entity Slide from EnhavoSliderBundle.

Add position property
---------------------

The first thing your resource needs to have is an integer property to save it's position in the order. In this example
it will be called ``position``.

.. code-block:: php

    class Slider {

        //...

        /**
         * @var integer
         **/
        protected position;

        /**
         * @param integer $position
         */
        public function setPosition($position)
        {
            $this->position = $position;
        }

        /**
         * @return integer
         */
        public function getPosition()
        {
            return $this->position;
        }

        //...

    }

This property also needs to be added to the Doctrine definitions, of course.

Generate routes
---------------

If you are creating a new resource rather than modifying an existing one, you can use the route generator command
(`see CRUD Routing generator`_). It has an optional parameter ``sorting`` that, if set to the property name defined
above, adds route configurations for sortable resources.

.. _see CRUD Routing generator: /book/routing/route-generator.html

Add route changes manually
--------------------------

If you are not creating a new resource but rather modifying an existing one, here are the route configurations to
do manually to activate sortable behaviour.

1. Add routes for moving items up and down
------------------------------------------

There are two routes specifically for moving the resource item up and down in order to change the sorting.
These are not present by default, they are only needed for sortable resources.

.. code-block:: yaml

    enhavo_slider_slide_move_up:
        options:
            expose: true
        path: /enhavo/slider/slide/move-up
        methods: [POST]
        defaults:
            _controller: enhavo_slider.controller.slide:moveUpAction
            _sylius:
                sortable_position: position # Property name
            _viewer:
                sorting: desc               # "desc" means higher values first


.. code-block:: yaml

    enhavo_slider_slide_move_down:
        options:
            expose: true
        path: /enhavo/slider/slide/move-down
        methods: [POST]
        defaults:
            _controller: enhavo_slider.controller.slide:moveDownAction
            _sylius:
                sortable_position: position # property name
            _viewer:
                sorting: desc               # "desc" means higher values first

2. Modify table route
---------------------

The table route defines the view where the user can see a table of all the resource items. You need to modify this
route so that the items appear in the right order. Also you have to add an extra column to the table to display arrow
buttons for moving the item.

.. code-block:: yaml

    enhavo_slider_slide_table:
        options:
            expose: true
        path: /enhavo/slider/slide/table/{page}
        methods: [GET]
        defaults:
            page: 1
            _controller: enhavo_slider.controller.slide:tableAction
            _sylius:
                template: EnhavoAppBundle:Resource:table.html.twig
                sorting:                    #
                    position: desc          # [property name]:[sort order], can be "desc" or "asc"
            _viewer:
                table:
                    sorting:                                                    #
                        sortable: true                                          # true to activate
                        move_up_route: enhavo_slider_slide_move_up              # route defined above
                        move_down_route: enhavo_slider_slide_move_down          # route defined above
                    columns:
                        id:
                            label: id
                            property: id
                            width: 1
                        title:
                            label: title
                            property: title
                            width: 10
                        position:                                               # column with arrows
                            label: position                                     # table headline
                            property: position                                  # property name
                            width: 1                                            #
                            widget: EnhavoAppBundle:Widget:position.html.twig   # widget rendering arrows

Commented lines are new.

3. Modify create route
----------------------

If a new item of the resource is created, it needs an initial value for its sorting position. Therefore, you also
need to modify the create route.

.. code-block:: yaml

    enhavo_slider_slide_create:
        options:
            expose: true
        path: /enhavo/slider/slide/create
        methods: [GET,POST]
        defaults:
            _controller: enhavo_slider.controller.slide:createAction
            _sylius:
                template: EnhavoAppBundle:Resource:create.html.twig
            _viewer:
                sorting:                #
                    sortable: true      # true to activate sorting
                    position: position  # property name
                    initial: max        # initial value, can be "max" or "min"

Commented lines are new.

If the value of ``initial`` is **"max"** (default), the newly created item will have an initial position value that is
the current maximum value plus one. If your sorting order defined in previous routes is **"desc"**, this means that the
new item will be the new first element, else it will be the last. A value of **"min"** will set the initial value to 0
and shift all existing items up by one, which can be slow for large amounts of data and is not recommended.
