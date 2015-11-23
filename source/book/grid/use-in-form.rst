Use in form
===========

You add the form type ``enhavo_content`` in your form.

.. code-block:: php

    $builder->add('content', 'enhavo_content');

Option Types
------------

.. code-block:: php

    $builder->add('content', 'enhavo_content', array(
        'types' => array(
            array('type' => 'text', 'label' => 'Text'),
            array('type' => 'picture', 'label' => 'Bild'),
            array('type' => 'video')
        )
    ));

If it is empty all items will be loaded. But if you want you can set explicit the types
which should be available. The parameter ``label`` is optional and if its not set
the standard label will be used, which is also configured in the configuration.
