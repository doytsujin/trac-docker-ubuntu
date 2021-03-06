# trac-ubuntu

[![](https://images.microbadger.com/badges/version/mastermindg/trac-ubuntu.svg)](https://hub.docker.com/r/mastermindg/trac-ubuntu/ "Get your own version badge on microbadger.com")
[![](https://images.microbadger.com/badges/image/mastermindg/trac-ubuntu.svg)](https://hub.docker.com/r/mastermindg/trac-ubuntu/)
[![Docker Hub](http://img.shields.io/docker/pulls/mastermindg/trac-ubuntu.svg)](https://hub.docker.com/r/mastermindg/trac-ubuntu/)

This repo builds a Docker container (based on Ubuntu Trusty) running [Trac](http://trac.edgewall.org),
which is an enhanced wiki and issue tracking system for software development
projects. Trac uses a minimalistic approach to web-based software project
management. It helps developers write great software while staying out of
the way. Trac should impose as little as possible on a team's established
development process and policies.

This installation of Trac uses AccountManager with LoginModule to allow logging in via the Web UI versus logging in with basic HTTP authentication. Eventually extensions will be added to enable LDAP and other forms of authentication.

# How to get the image

* Build it using Dockerfile

    ```ssh
    $ git clone https://github.com/mastermindg/trac-docker-ubuntu
    $ cd trac-docker-ubuntu
    $ docker build -t trac ./
    ```

* just pull it from Dockerhub

    ```
    $ docker pull mastermindg/trac-ubuntu
    ```


# How to run the container

## Quick Start

Just run

```
$ docker run -d -p 80:80 --name my_trac mastermindg/trac-ubuntu
```

After several seconds, you can visit the web page at
<http://localhost>

The Dockerfile comes with a number of environment variables that can be set at build time or at run time:

## Environment Variables Explanations

Most of below

* `TRAC_ADMIN_NAME` (default is `trac_admin`):

    the admin username of Trac

* `TRAC_ADMIN_PASS` (default is `passw0rd`):

    the admin password of Trac

* `TRAC_PROJECT_NAME` (default is `trac_project`):

    the Trac project name

* `TRAC_DIR` (default is `/trac`):

    This directory stores all the data and configurations. You can bind a volume
    when starting a container.

* `TRAC_INI` (default is `$TRAC_DIR/conf/trac.ini`):

    This ini file will be automatically generated by the container.
    Also you can made some customizations based on your needs.

* `DB_LINK` (default is `sqlite:db/trac.db`):

    A database system is needed. The database can be either `SQLite`,
    `PostgreSQL` or `MySQL`.

    Please refer <https://trac.edgewall.org/wiki/TracInstall#MandatoryDependencies>
    for more detailed infomation.

    * For the PostgreSQL database

        See [DatabaseBackend](https://trac.edgewall.org/intertrac/DatabaseBackend%23Postgresql) for details.

    * For the MySQL database

        Trac works well with MySQL.
        Given the caveats and known issues surrounding MySQL,
        read the [MySqlDb](https://trac.edgewall.org/intertrac/MySqlDb) page
        before creating the database.
        
        * Build it for use with a MySQL database

        ```ssh
        $ git clone https://github.com/mastermindg/trac-docker-ubuntu
        $ cd trac-docker-ubuntu
        $ docker build -t trac --build-arg DB_LINK="mysql://trac:trac@mysql:3306/trac" .
        ``` 
        OR
        * Run it with a MySQL Database
        ```ssh
        $ docker run -d -p 80:80 --name trac -e DB_LINK="mysql://trac:trac@mysql:3306/trac" mastermindg/trac-ubuntu
        ``` 
        


This can be run off of a mount to persist the data:

```
docker run -d --name trac -p 80:80 -v /home/me/trac:/trac -e TRAC_PROJECT_NAME=custom_name mastermindg/trac-ubuntu
```

# Reference

* [Trac Official Doc](https://trac.edgewall.org/wiki/TracGuide)
