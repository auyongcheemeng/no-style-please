---
layout: post
title:  "php-fpm with mysql/mariadb server-client api version mismatch"
date:   2017-01-31
categories: server
tags: raspbian php mysql mariadb
---
Well it has been a while since I've needed to set up any new servers with php and mysql. It's all old rusty on my end since I've been doing other projects besides web dev lately. 

I discovered the error message when I trying upgrade an internal wordpress site on a raspi server. The error reads something like this:

    mysql_connect(): Headers and client library minor version mismatch

Hmm...curiously I dug around and found out that the PHP support for mysql (php5-mysql) was compiled using an earlier version of mysql, mysql has since been updated to a later version [[ServerFault](https://serverfault.com/questions/228532/mysql-headers-and-client-library-minor-version-mismatch)]

`apt-get install mysql-server` results in: 

    The following packages have unmet dependencies:
    mysql-server : Depends: mysql-server-5.5 but it is not going to be installed
    E: Unable to correct problems, you have held broken packages.

Okay..., the we try `apt-get install mysql-server-5.5` and get:

    The following packages have unmet dependencies:
    mysql-server-5.5 : Depends: mysql-client-5.5 (>= 5.5.54-0+deb8u1) but it is not going to be installed
    PreDepends: mysql-common (>= 5.5.54-0+deb8u1) but it is not going to be installed
    E: Unable to correct problems, you have held broken packages.

Sigh...alright, lets try installing `mysql-server-5.6`

    Package mysql-server-5.6 is not available, but is referred to by another package.
    This may mean that the package is missing, has been obsoleted, or is only available from another source
    However the following packages replace it:
      mariadb-server-5.5 mariadb-server-10.0

We get a hint here, turnes out its been replaced by mariadb. (At least on the rasbian jessie repo that I'm on). Hence, I ended up geting rid of the `mysql-server` installation and went with a `mariadb-server-10.0` install

After upgrading, mariadb works and upgraded al my db tables, all looks fine...but it turns out that, the version mismatch still persists. More googling reveals a [MariaDB knowledge base](https://mariadb.com/kb/en/mariadb/installation-issues-with-php5/) article with some suggested solutions. 

I opted for option #1 that is:

    apt-get install php5-mysqlnd

And voila, no more errors.
