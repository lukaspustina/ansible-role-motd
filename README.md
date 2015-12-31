motd
=========

Creates a dynamic motd.

Example:
```
[lukas@cake]  ~  ➜  ssh heimbot
 _          _           _           _
| |__   ___(_)_ __ ___ | |__   ___ | |_
| '_ \ / _ \ | '_ ` _ \| '_ \ / _ \| __|
| | | |  __/ | | | | | | |_) | (_) | |_
|_| |_|\___|_|_| |_| |_|_.__/ \___/ \__|


Welcome to Raspbian GNU/Linux 8.0 (jessie) (4.1.7-v7+).

System information as of Thu Dec 31 13:44:31 CET 2015

System load:	0.21	IP Address:	192.168.101.120
Memory usage:	9.8%	System uptime:	17:27 hours
Usage on /:	4%	Swap usage:	0.0%
Local Users:	1	Processes:	88

● apache2: active (running) since Wed 2015-12-30 19:58:29 CET; 17h ago
● fhem: active (running) since Wed 2015-12-30 22:48:49 CET; 14h ago
● homebridge: active (running) since Thu 2015-12-31 08:29:10 CET; 5h 15min ago

Last login: Thu Dec 31 13:43:52 2015 from cake.fritz.box
```

Requirements
------------

None

Role Variables
--------------

`_motd` contains an optional list of services which should be status checked. See example playbook below. The place holder `@@NAME@@` is replaced by concrete service names and can be used to write individual service check commands.

Dependencies
------------

None

Example Playbook
----------------

Example using systemd for service management.

```
    - hosts: servers
      vars:
        MOTD:
          services:
            command: 'systemctl status @@NAME@@ | sed -ne "/service -\|Active/ p" | sed -e "N;s/\n / /" -e "s/^\(.*\).service.*Active: \(.*\)/\1: \2/"'
            services:
              - apache2
              - fhem
              - homebridge
      roles:
        - { role: motd, tags: [ 'motd' ], _motd: "{{ MOTD }}" }
```

License
-------

GPL

Author Information
------------------

Initially created by Lukas Pustina [@drivebytesting](https://twitter.com/drivebytesting).

