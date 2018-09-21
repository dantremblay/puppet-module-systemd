# Puppet Systemd module

This module manages SystemD services files


## Comptability

This module has been tested to work on the following systems.

* EL 7


## Parameters

### class systemd

units
-----
define the unit parameters

- *Default*: undef

## define systemd::unit

ensure
------
ensure attribute for unit file resource.  Valid values are 'present' and 'absent'.

- *Default*: 'present'

systemd_path
------------
Path to systemd unit files.

- *Default*: '/etc/systemd/system'

unit_after
----------
List of units that must be started before the unit being configured.

- *Default*: undef

unit_before
-----------
List of units that must be started after the unit being configured.

- *Default*: undef

unit_description
----------------
A free-form string describing the unit.

- *Default*: undef

unit_requires
-------------
List of units that will be activated as well as the unit being configured.

- *Default*: undef

environment
-----------
Set environment variables for executed processes. Takes a list of space-separated list of variable assignments.

- *Default*: undef

group
-----
group running the service

- *Default*: undef

user
----
user running the service

- *Default*: undef

workingdirectory
----------------
defines on which directory the service will be launched from.

- *Default*: undef

service_type
------------
configures the process start-up type for this service unit.  Valid values are: 'simple', 'forking', 'oneshot', 'dbus', 'notify' and 'idle'.

- *Default*: 'simple'

service_timeoutstartsec
-----------------------
configures the time to wait for start-up. If a daemon service does not signal start-up completion within the configured time, the service will be considered failed and will be shut down again. Takes a unit-less value in seconds, or a time span value such as "5min 20s".

- *Default*: undef

service_restart
---------------
configures whether the service shall be restarted when the service process exits, is killed, or a timeout is reached.

- *Default*: undef

service_restartsec
------------------
configures the time to sleep before restarting a service (as configured with Restart=). Takes a unit-less value in seconds, or a time span value such as "5min 20s".

- *Default*: undef

service_execstartpre
--------------------
additional commands that are executed before the command in service_execstart

- *Default*: undef

service_execstart
-----------------
commands with their arguments that are executed when this service is started.

- *Default*: undef

service_execstop
----------------
commands to execute to stop the service started via service_execstart

- *Default*: undef

install_wanteby
---------------
the most common way to specify how a unit should be enabled. This directive allows you to specify a dependency relationship in a similar way to the Wants= directive does in the [Unit] section.

- *Default*: undef

## Sample Usage

Define service 'myservice' as a systemd unit.

```
systemd::units:
  'myservice':
    unit_description: 'This is my service'
    service_timeoutstartsec: 0
    service_execstartpre: [ "-/usr/bin/command --kill", "-/usr/bin/command --rm" ]
    service_execstart: "/usr/bin/command run --fqdn %{fqdn}"
    service_execstop: "/usr/bin/command --kill"
    install_wantedby: 'multi-user.target'
```
