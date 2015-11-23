Rendering
=========

Now you want to render your content? This is a very easy task.
Just use the twig function ``content_render``. This function has got
two parameter. The first one is the content data, which you should pass
to the template. The second one is optional and is used to render a
different template set. For further information read the section ``Render sets``

If you use the ``content_render`` with one parameter, then the template
for the item is rendered which is defined in your configuration.

.. code-block:: twig

    content_render(content)

    {# render with specific set #}
    content_render(content, 'page')


Render sets
-----------

If you are in the situation that you have two render to different templates for the same item type
in your application, then the render sets will help you to implement this.

In your configuration you can define a render set. Here we call it ``page``.
Now we can define for each item a new template. If you don't define a template
for an item under this set, then the standard template will be used.

.. code-block:: yaml

    enhavo_content:
        render:
            sets:
                page:
                    picture: enhavoProjectBundle:ItemType:page/picture.html.twig
                    text: enhavoProjectBundle:ItemType:page/text.html.twig