# Setting up Oracle

Given below are the steps you need to follow in order to use an Oracle database for cluster coordination in a Micro Integrator cluster.

## Setting up the database and users

Follow the steps below to set up an Oracle database.

1.  Create a new database by using the Oracle database configuration
    assistant (dbca) or manually.
2.  Make the necessary changes in the Oracle
    `           tnsnames.ora          ` and
    `           listner.ora          ` files in order to define
    addresses of the databases for establishing connections to the newly
    created database.
3.  After configuring the `           .ora          ` files, start the
    Oracle instance using the following command:

     `sudo /etc/init.d/oracle-xe restart`

4.  Connect to Oracle using SQL\*Plus as SYSDBA as follows:

    `./$<ORACLE_HOME>/config/scripts/sqlplus.sh sysadm/password as SYSDBA`

5.  Connect to the instance with the username and password using the
    following command:

    `connect`

6.  As SYSDBA, create a database user and grant privileges to the user
    as shown below:

    ```bash
    Create user <USER_NAME> identified by <PASSWORD> account unlock;
    grant connect to <USER_NAME>;
    grant create session, create table, create sequence, create trigger to <USER_NAME>;
    alter user <USER_NAME> quota <SPACE_QUOTA_SIZE_IN_MEGABYTES> on '<TABLE_SPACE_NAME>';
    commit;
    ```

7.  Exit from the SQL\*Plus session by executing the
    `          quit         ` command.

## Setting up the JDBC driver

1.  Copy the Oracle JDBC libraries (for example, \<
    `          ORACLE_HOME/jdbc/lib/ojdbc14.jar)         ` to the `MI_HOME/lib/`
    directory.
2.  Remove the old database driver from the
    `MI_HOME/repository/components/dropins/         `
    directory.

!!! Tip
    If you get a "`timezone region not found"` error when using the `         ojdbc6.jar        ` file with the Micro Integrator, set the Java property as follows: `export JAVA_OPTS="-Duser.timezone='+05:30'"` the value of this property should be the GMT difference of the country. If it is necessary to set this property permanently, define it inside the `micro-integrator.sh        ` as a new `JAVA_OPT` property.

## Connecting to the database

Add the following parameters to the `deployment.toml` file in the `MI_HOME/conf` directory.

```toml
[[datasource]]
id = "WSO2_COORDINATION_DB"
url= "jdbc:oracle:thin:@SERVER_NAME:PORT/SID"
username="root"
password="root"
driver="oracle.jdbc.OracleDriver"
pool_options.maxActive=50
pool_options.maxWait = 60000
pool_options.testOnBorrow = true
```

Find more parameters for [connecting to the database](../../../../references/config-catalog/#database-connection).