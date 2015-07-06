Installation
============

To create a project with the enhavo, you just need the following composer command.

.. code-block:: bash

    composer create-project enhavo/enhavo-project project-name dev-master

After you have installed enhavo successfully over composer and set the correct
database setting into your parameters.yml you can update your database

.. code-block:: bash

    app/console doctrine:schema:update --force
    app/console doctrine:fixtures:load

Now you can add your own bundle to the project. Just generate one over symfony.

.. code-block:: bash

    app/console generate:bundle