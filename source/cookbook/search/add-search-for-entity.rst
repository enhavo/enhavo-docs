Add search for an entity
========================

To make an entity searchable, just follow this steps.

1) Add search to enhavo.yml
2) Start cron and run command
3) Create the search.yml

Add search to enhavo.yml
------------------------

Just copy the following code into your ``enhavo.yml``

.. code-block:: yml

    enhavo_search:
        search:
            template: EnhavoSearchBundle:Search:render.html.twig
            strategy: reindex
            search_engine: enhavo_search_search_engine
            index_engine: enhavo_search_index_engine

Here you tell enhavo which template should be rendered for the search-field,
which indexing strategy should be used and which engines do the work of indexing and searching.
For the indexing strategy you can choose between index (which means every entry of your entity gets indexed immediately), index_new (which means every new entry  of your entity gets indexed immediately) and reindex (which means the entries of your entity get indexed when the reindex function has been called).

Start cron and run command
--------------------------

If you use the index_new or reindex strategy you have to run the following command:

.. code-block:: bash

    app/console enhavo:search:index

The easiest way you can do that is with a cron job. ...


Create the search.yml
---------------------

Finally you can create the search.yml for your entity. Put the search.yml into ``AcmeBundle/Resource/config``.

.. code-block:: yml

    Acme\AcmeBundle\Entity\Acme:
        properties:
            title:
                - Plain:
                    weight: 10
                    type: title
            text:
                - Html:
                    type: text
                    weights:
                      h1: 12
                      h2: 10
                      p: 7
            tag:
                - Collection:
                    - Plain:
                        weight: 3
                        type: tag
            category:
                - Collection:
                    entity: Enhavo\Bundle\CategoryBundle\Entity\Category
            grid:
                - Model

Under `properties` you can define the fields of your entity that should be indexed.
Under each field you tell the search engine what kind of content is in the current field.
If you have just a plain text you choose ``Plain`` field:

.. code-block:: yml

    title:
        - Plain:
            weight: 10
            type: title

If there is a HTML text which contains HTML-tags, you should choose the ``Html`` field.

.. code-block:: yml

    text:
        - Html:
            type: text
            weights:
              h1: 12
              h2: 10
              p: 7

With the `type` you can set the type as which the field gets stored in the database and whith the `weight` you choose the weight of the field compared to all the other fields.
If you have the `Html` field you can give weights to each HTML-tag (if you just skip the `weights` there are default weights for the HTML-tags).

If your field is a ``Collection``, you can choose between to types.

.. code-block:: yml

    tag:
        - Collection:
            - Plain:
                weight: 3
                type: tag
    category:
        - Collection:
            entity: Enhavo\Bundle\CategoryBundle\Entity\Category

The first type means that the collection are just fiels of type text or HTML.
The second one means that your collection consists of an other entity. In this case the other entity has to have a search.yml, too.

The last field is a ``Model``.

.. code-block:: yml

    grid:
        - Model

In this case the search engine takes the class of the given field and looks for the search.yml in belonging bundle.
This assumes that the bundle has a own search.yml.