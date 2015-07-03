Wysiwyg
=======

This section explain how you can configure your wysiwyg editor system wide
and in some special cases. The enhavo use the ``TinyMCE`` editor, if
you are familiar with its settings you can easily configure it, otherwise
you should also read the TinyMCE `docs for configuration`_.

.. _docs for configuration: http://www.tinymce.com/wiki.php/Configuration


Configuration
-------------

You can find the system wide configuration under ``app/config/wysiwyg.yml``.
All settings here a equivalent to the ``TinyMCE`` configuration, mentioned above.
Note that this is a yaml file and the TinyMCE configuration is a Javascript Object or
JSON, but yaml can be translated one to one JSON.

This configuration are available:

.. _height: http://www.tinymce.com/wiki.php/Configuration:height
.. _formats: http://www.tinymce.com/wiki.php/Configuration:formats
.. _style_formats: http://www.tinymce.com/wiki.php/Configuration:style_formats
.. _toolbarN: http://www.tinymce.com/wiki.php/Configuration:toolbar%3CN%3E
.. _content_css: http://www.tinymce.com/wiki.php/Configuration:content_css

- height_
- toolbarN_
- style_formats_
- formats_
- content_css_

.. code-block:: yaml

    height: 150

    toolbar1: "undo redo | bold italic underline strikethrough subscript superscript removeformat | link styleselect"

    toolbar2: "table | alignleft aligncenter alignright alignjustify | bullist numlist outdent indent | code"

    style_formats:
        - {title: 'Bold text', inline: 'b'}
        - {title: 'Red text', inline: 'span', styles: {color: '#ff0000'}}
        - {title: 'Red header', block: 'h1', styles: {color: '#ff0000'}}
        - {title: 'Example 1', inline: 'span', classes: 'example1'}
        - {title: 'Example 2', inline: 'span', classes: 'example2'}
        - {title: 'Table styles'}
        - {title: 'Table row 1', selector: 'tr', classes: 'tablerow1'}

    formats:
          alignleft: {selector: 'p,h1,h2,h3,h4,h5,h6,td,th,div,ul,ol,li,table,img', classes: 'left'}
          aligncenter: {selector: 'p,h1,h2,h3,h4,h5,h6,td,th,div,ul,ol,li,table,img', classes: 'center'}
          alignright: {selector: 'p,h1,h2,h3,h4,h5,h6,td,th,div,ul,ol,li,table,img', classes: 'right'}
          alignfull: {selector: 'p,h1,h2,h3,h4,h5,h6,td,th,div,ul,ol,li,table,img', classes: 'full'}
          bold: {inline: 'span', 'classes': 'bold'}
          italic: {inline: 'span', 'classes': 'italic'}
          underline: {inline: 'span', 'classes': 'underline', exact: true}
          strikethrough: {inline: 'del'}
          customformat: {inline: 'span', styles: {color: '#00ff00', fontSize: '20px'}, attributes: {title: 'My custom format'}}

    content_css: ~ #read the text below

**content_css**

For the content_css, we need assets/assetics so you need to use the @ syntax

.. code-block:: yaml

    #multiple files
    content_css:
      - '@enhavoProjectBundle/Resources/public/css/styleOne.css'
      - '@enhavoProjectBundle/Resources/public/css/styleTwo.css'

.. code-block:: yaml

    #single file
    content_css: '@enhavoProjectBundle/Resources/public/css/styleOne.css'


FormType
--------

If you need a special configuration just for one form, you can override or filter
some settings in the FormType option array.

- **formats**: Needs an array, where you can list the formats which should be shown.
- **height**: Overwrite the height
- **toolbar1**: Overwrite the toolbar1
- **toolbar2**: Overwrite the toolbar2
- **content_css**: Overwrite the content_css, this could be an array or a string (Use @ Syntax)

.. code-block:: php

    $builder->add('text', 'wysiwyg', array(
        'formats' => array('Bold text', 'Red text'),
        'height' => 300,
        'toolbar1' => '',
        'toolbar2' => ''
        'content_css' => array(
            '@enhavoProjectBundle/Resources/public/css/styleOne.css'
        )
    );



