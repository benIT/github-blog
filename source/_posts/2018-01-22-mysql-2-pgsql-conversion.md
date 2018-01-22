---
title: mySQL to postgreSQL schema conversion
categories:
    - mySQL
    - pgSQL
tags:

---

## Purpose

I was looking for a tool that convert a mysql db to a pgsql one.
[philipsoutham/py-mysql2pgsql](https://github.com/philipsoutham/py-mysql2pgsql) does the trick and saved my day!

## Install

    sudo apt-get install python-pip
    pip install py-mysql2pgsql

## Configure

Edit configuration in `mysql2pgsql.yml`


    # if a socket is specified we will use that
    # if tcp is chosen you can use compression
    mysql:
     hostname: localhost
     port: 3306
     socket: /var/run/mysqld/mysqld.sock
     #socket: /tmp/mysql.sock
     username: emedia
     password: emedia
     database: emedia
     compress: false
    destination:
     # if file is given, output goes to file, else postgres
     file: /vagrant/shared/migrationMysql2Pgsql.sql
     postgres:
      hostname: localhost
      port: 5432
      username: mysql2psql
      password:
      database: mysql2psql_test

    # if tables is given, only the listed tables will be converted.  leave empty to convert all tables.
    only_tables:
    - lti2_consumer
    - lti2_context
    - lti2_nonce
    - lti2_resource_link
    - lti2_share_key
    - lti2_tool_proxy
    - lti2_user_result
    # if exclude_tables is given, exclude the listed tables from the conversion.
    #exclude_tables:
    #- table3
    #- table4

    # if supress_data is true, only the schema definition will be exported/migrated, and not the data
    supress_data: true

    # if supress_ddl is true, only the data will be exported/imported, and not the schema
    supress_ddl: false

    # if force_truncate is true, forces a table truncate before table loading
    force_truncate: false
