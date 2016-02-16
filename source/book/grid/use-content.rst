Using the content
=================


Adding to the model
-------------------

To add a property of type content to your resource model, add a one-to-one association to your doctrine definition
and update your entity.

.. code-block:: yaml
    oneToOne:
        content:
            cascade: ['persist', 'refresh', 'remove']
            targetEntity: Enhavo\Bundle\GridBundle\Entity\Content

.. code-block:: php
    <?php

    //...

    class Foo {

    //...

    protected $content;

    public function getContent() {...}
    public function setContent(...) {...}

    //...

    }


Adding to form
--------------

To properly edit a property of the type "content" in your form, use the form type ``enhavo_grid``.

.. code-block:: php

    $builder->add('content', 'enhavo_grid');


Types of content
----------------

If you don't add any options, all item types configured in app/config/enhavo.yml will be available in the form. You
can restrict the available types by setting the option ``items``.

.. code-block:: php

    $builder->add('content', 'enhavo_content', array(
        'items' => array(
            array('type' => 'text'),
            array('type' => 'picture', 'label' => 'Picture'),
            array('type' => 'video', 'label' => 'label.video', 'translationDomain' => 'AcmeFooBundle')
        )
    ));

The parameter ``label`` is optional, it's default value can be configured in app/config/enhavo.yml.
The parameter ``translationDomain`` defaults to "EnhavoGridBundle" if it is not set.
