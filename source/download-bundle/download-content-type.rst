Download Content Type
=====================

The ``DownloadBundle`` has a content item, which can be activated. This article show how you do this.

Just add the item to ``esperanto_content``.

.. code-block:: yaml

    esperanto_content:
        items:
            download:
                model: esperanto\DownloadBundle\Entity\DownloadItem
                form: esperanto\DownloadBundle\Form\Type\DownloadItemType
                repository: esperantoDownloadBundle:DownloadItem
                template: esperantoDownloadBundle:Item:download.html.twig
                label: Download

And the fields.html into the twig config.

.. code-block:: yaml

    twig:
        form:
            resources:
                - 'esperantoDownloadBundle:Item:fields.html.twig'
