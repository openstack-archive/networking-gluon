2. Edit the ``/etc/networking-gluon/networking-gluon.conf`` file and complete the following
   actions:

   * In the ``[database]`` section, configure database access:

     .. code-block:: ini

        [database]
        ...
        connection = mysql+pymysql://networking-gluon:NETWORKING-GLUON_DBPASS@controller/networking-gluon
