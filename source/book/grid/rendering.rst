Rendering
=========

To render the content in the frontend, you can use the twig function ``content_render``. This function has
two parameters. The first one is the content object. The second one is optional and is used to render a
different template set. For further information read the section ``Render sets`` below.

If you use ``content_render`` with one parameter, it will render the default template for the item which is defined
in your configuration in app/config/enhavo.yml.

.. code-block:: twig

    content_render(content)

    {# render with specific set #}
    content_render(content, 'page')


Render sets
-----------

If you want to render two different templates for the same item type in your application, then you can use render sets.

In the configuration in app/config/enhavo.yml you can define render sets. In this example, we defined one called
``page``. Now we can define a new template for each item. Items without a defined template will use the default
template.

.. code-block:: yaml

    enhavo_content:
        render:
            sets:
                page:
                    picture: enhavoProjectBundle:ItemType:page/picture.html.twig
                    text: enhavoProjectBundle:ItemType:page/text.html.twig
