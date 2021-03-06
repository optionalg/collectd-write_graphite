write\_graphite
==============

An output plugin for [collectd](http://collectd.org).

*NOTE* This work has been merged into [collectd](http://collectd.org/) as of version 5.1. I strongly suggest using the native client, as octo has done great things with it and I no longer plan on maintaining this code. Thanks!

Description
-----------

The write\_graphite plugin sends data to [Carbon](http://graphite.wikidot.com/carbon), the [Graphite](http://graphite.wikidot.com) backend. Data is sent in 4K blocks over TCP to Carbon. I could possibly have named this plugin write\_carbon.


Installation
------------

First, modify the variables at the top of the Makefile to fit your system. (I use FreeBSD.) Then continue making the project as usual. During the initial make, collectd will be downloaded and configured to provide the neccesary libtool script.

    $ git clone git@github.com:jssjr/collectd-write_graphite.git
    $ cd collectd-write_graphite
    $ make
    $ sudo make install


Configuration
-------------

Enable the plugin in collectd.conf by adding:

    LoadPlugin write_graphite

Configure the plugin to match your carbon configuration.

    <Plugin write_graphite>
      <Carbon>
        Host "localhost"
        Port "2003"
        Prefix "collectd."
      </Carbon>
    </Plugin>

Restart collectd to load the new plugin.

### Available Carbon Configuration Directives

*    Host *required*

     The hostname of the Carbon collection agent.

*    Port *required*

     The port used by the Carbon collect agent.

*    Prefix

     The prefix string prepended to the hostname that is sent to Carbon. Use dots (.) to create folders. A good choise might be "collectd." or "servers."

*    Postfix

     The postfix string appended to the hostname sent to Carbon.

*    DotCharacter

     The character used to replace dots (.) in a hostname or datasource name. Defaults to an underscore.
