Get Started
===========

To create a project with enhavo, you just need to run the following composer command.

.. code-block:: bash

    composer create-project enhavo/enhavo-project project-name dev-master

After you have successfully installed enhavo via composer and set up the database settings in your parameters.yml
you can update your database schema.

.. code-block:: bash

    app/console doctrine:schema:update --force
    app/console doctrine:fixtures:load

Now you can add your own bundles to the project, for example by using the Symfony generate commands.

.. code-block:: bash

    app/console generate:bundle
