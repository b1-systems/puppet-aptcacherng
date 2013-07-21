# aptcacherng

#### Table of Contents

1. [Overview](#overview)
2. [Setup](#setup)
    * [What aptcacherng affects](#what-aptcacherng-affects)
    * [Beginning with aptcacherng](#beginning-with-aptcacherng)
3. [Usage](#usage)
4. [Limitations](#limitations)
5. [Development](#development)

## Overview

A puppet module to manage an [apt-cacher-ng](https://www.unix-ag.uni-kl.de/~bloch/acng/) service and its configuration.  Applying `aptcacherng` to a node will configure the node to act as a caching proxy for *apt* (and other) package management systems.

## Setup

### What aptcacherng affects

Use of `aptcacherng` causes installation of the `apt-cacher-ng` package, generation of the config file `/etc/apt-cacher-ng/acng.conf`, and the `apt-cacher-ng` service to run and be enabled.

### Beginning with aptcacherng

This module is very straightforward to use.

## Usage

Simply declaring the `aptcacherng` class for a node, will apply the class using standard `apt-cacher-ng` defaults:

* CacheDir: /var/cache/apt-cacher-ng
* LogDir: /var/log/apt-cacher-ng
* Port: 3142
* ReportPage: acng-report.html
* ExTreshold: 4

*All* `apt-cacher-ng` config file directives are available as parameters to the `aptcacherng` class.  For example, to change the directory where `apt-cacher-ng` will store its cache:

    class {'apt':
        cachedir => '/data/apt/apt-cacher-ng'
    }

Or, in a YAML hiera data source—for example—you could make use of automatic parameter lookups like so:

    ---
    classes:
      - aptcacherng

    aptcacherng::cachedir: "/data/apt/apt-cacher-ng"

If you wish to make `aptcacherng` install a specific `apt-cacher-ng` package, you may pass the `packagename` string parameter when declaring the class.

If you're using the `puppetlabs-apt` module, telling `apt` to use your `apt-cacher-ng` service is simple.  For example:

    class {'apt':
        proxy_host => 'server.name.com',
        proxy_port => '3142',
    }

## Limitations

Only debian based distributions are currently supported.

## Development

Development takes place in the [markhellewell-aptcacherng](https://github.com/markhellewell/markhellewell-aptcacherng) GitHub repository.  Pull Requests happily accepted.
