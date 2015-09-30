# sentry-deb

The goal of this project is to package [sentry](https://getsentry.com)
for [debian](https://www.debian.org). It leverages
[dh-virtualenv](https://github.com/spotify/dh-virtualenv) to perform
the actual work. The primary OS target is debian 8 "jessie"; It might
or might not work on other debian and debian based systems.

## Usage

From the *same OS version* as your target, do:

    $ git clone git@github.com:dhatim/sentry-deb.git
    $ cd sentry-deb/sentry-7.7.0
    $ dpkg-buildpackage -us -uc
    $ cd ..
    $ ls -1
    README.md
    sentry-7.7.0
    sentry_7.7.0.dsc
    sentry_7.7.0.tar.gz
    sentry_7.7.0_amd64.changes
    sentry_7.7.0_amd64.deb

## some more details

### sentry

The target sentry version is 7.7.0. postinst calls `sentry init
/usr/share/python/sentry/sentry.conf.py` if this file doesn't exist
already, so as to provide a sample configuration file.

### postgresql

The package adds a dependency on the postgresql driver, so it is ready
to use with a postgresql database.

### supervisor

The package is made to depend on supervisor, and provides a suitable
supervisor configuration file so that sentry server and workers start
as services, managed by supervisor.

### service

Please note that *The sentry service won't start by default on package
installation.*.  You'll have to configure what needs to be configured,
and tickle supervisor so it picks up the changes.

