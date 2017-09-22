Prerequisites
-------------

Before you install and configure the Gluon Service Plugin service,
you must create a database, service credentials, and API endpoints.

#. To create the database, complete these steps:

   * Use the database access client to connect to the database
     server as the ``root`` user:

     .. code-block:: console

        $ mysql -u root -p

   * Create the ``networking-gluon`` database:

     .. code-block:: none

        CREATE DATABASE networking-gluon;

   * Grant proper access to the ``networking-gluon`` database:

     .. code-block:: none

        GRANT ALL PRIVILEGES ON networking-gluon.* TO 'networking-gluon'@'localhost' \
          IDENTIFIED BY 'NETWORKING-GLUON_DBPASS';
        GRANT ALL PRIVILEGES ON networking-gluon.* TO 'networking-gluon'@'%' \
          IDENTIFIED BY 'NETWORKING-GLUON_DBPASS';

     Replace ``NETWORKING-GLUON_DBPASS`` with a suitable password.

   * Exit the database access client.

     .. code-block:: none

        exit;

#. Source the ``admin`` credentials to gain access to
   admin-only CLI commands:

   .. code-block:: console

      $ . admin-openrc

#. To create the service credentials, complete these steps:

   * Create the ``networking-gluon`` user:

     .. code-block:: console

        $ openstack user create --domain default --password-prompt networking-gluon

   * Add the ``admin`` role to the ``networking-gluon`` user:

     .. code-block:: console

        $ openstack role add --project service --user networking-gluon admin

   * Create the networking-gluon service entities:

     .. code-block:: console

        $ openstack service create --name networking-gluon --description "Gluon Service Plugin" gluon service plugin

#. Create the Gluon Service Plugin service API endpoints:

   .. code-block:: console

      $ openstack endpoint create --region RegionOne \
        gluon service plugin public http://controller:XXXX/vY/%\(tenant_id\)s
      $ openstack endpoint create --region RegionOne \
        gluon service plugin internal http://controller:XXXX/vY/%\(tenant_id\)s
      $ openstack endpoint create --region RegionOne \
        gluon service plugin admin http://controller:XXXX/vY/%\(tenant_id\)s
