Add content type
================

If you follow this step, you can add any content type easily to the cms.

1) Create an Entity
2) Create a FormType
3) Create a template file
4) Add configuration

In the following we add an example content type called youtube. In our case youtube type contains
these three parameter: ``url``, ``title`` and ``author``

Entity
------

An entity must implement the ``ItemTypeInterface``. Remember that a entity should
be a really doctrine entity. Cause the ContentBundle will call ``persists`` to this object.
If you use a non doctrine entity, then you will receive errors while trying to save the content.

.. code-block:: php

    <?php

    namespace enhavo\ProjectBundle\Entity;

    use enhavo\ContentBundle\Item\ItemTypeInterface;

    class Youtube implements ItemTypeInterface
    {
        private $id;
        private $url;
        private $title;
        private $author;

        public function getId()
        {
            return $this->id;
        }

        public function getUrl()
        {
            return $this->url;
        }

        public function setUrl($url)
        {
            $this->url = $url;
            return $this;
        }

        //...setter and getter for title and author
    }


FormType
--------

A FormType should extend from ``ItemFormType``.

.. code-block:: php

    <?php

    namespace enhavo\ProjectBundle\Form\Type;

    use enhavo\ContentBundle\Item\ItemFormType;
    use Symfony\Component\Form\FormBuilderInterface;
    use Symfony\Component\OptionsResolver\OptionsResolverInterface;

    class YoutubeType extends ItemFormType
    {
        public function buildForm(FormBuilderInterface $builder, array $options)
        {
            $builder->add('url', 'text');
            $builder->add('title', 'text');
            $builder->add('author', 'text');
        }

        public function setDefaultOptions(OptionsResolverInterface $resolver)
        {
            $resolver->setDefaults(array(
                'data_class' => 'enhavo\ProjectBundle\Entity\Youtube'
            ));
        }

        public function getName()
        {
            return 'enhavo_content_item_youtube';
        }
    }

If you want to change the style in your form you have to add a new block in separate twig file.

.. code-block:: yaml

    #fields.html.twig
    {% block enhavo_content_item_youtube_widget %}
    <div class="padding">
        {{ form_widget(form.url) }}
    </div>
        <div class="padding">
        {{ form_widget(form.title) }}
    </div>
        <div class="padding">
        {{ form_widget(form.author) }}
    </div>
    {% endblock %}

And this file, here ``fields.html.twig``, need to be add to the config.

.. code-block:: twig

    twig:
        form:
            resources:
                - 'enhavoProjectBundle:Form:fields.html.twig'

Template
--------

Just create a simple twig file somewhere in your bundle.
This template will be used the render this type in your
application. The entity which is connected to this type
will be passed to the template as the parameter ``data``.
In our case this will be an object from the ``Youtube`` class.

.. code-block:: twig

    {# enhavoProjectBundle:ItemType:youtube.html.twig #}

    <h2>{{ data.title }}<h2>
    <iframe width="560" height="315" src="{{ data.url }}" frameborder="0" allowfullscreen></iframe>
    <div>by {{ data.author }}</div>

Configuration
-------------

Finally you need to add the youtube type to the configuration under the section ``enhavo_content.items``.
The option ``label`` is optional and is used in the context menu where you can add a new item to your content.

.. code-block:: yaml

    enhavo_content:
        items:
            youtube:
                model: enhavo\ProjectBundle\Entity\Youtube
                form: enhavo\ProjectBundle\Form\Type\YoutubeType
                repository: enhavoProjectBundle:Youtube
                template: enhavoProjectBundle:ItemType:youtube.html.twig
                label: Youtube


