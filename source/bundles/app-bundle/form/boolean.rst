Boolean
=======

The ```enhavo_boolean``` helps for boolean fields and render a true and false radio selection.

FormType
--------

If you need a special configuration just for one form, you can override or filter
some settings in the FormType option array.

- **label_true**: label for field true
- **label_false**: label for field false
- **default**: If the value is null, you can configure here what to check. (true|false|null). If null no one will be checked (default setting)

.. code-block:: php

    $builder->add('public', 'enhavo_boolean', array(
        'label_true' =>  'label.yes',
        'label_false' => 'label.no',
        'default' => null
    );



