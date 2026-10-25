memcache-top
============

"top" for memcached - watch traffic and stats in real time, and see at a
glance when an instance is actually in trouble.  In the style of htop and
btop: quiet when everything is fine, yellow or red only when it is not.

Single Perl script, core modules only.  Speaks the memcached ``stats``
command over TCP.  Works with memcached 1.2.3 and later.

Interface in English, Portuguese and Spanish.

.. image:: docs/screenshot.png
   :alt: memcache-top showing an instance that is evicting, near max_connections and recently restarted

INSTALL
-------

::

   curl -O https://raw.githubusercontent.com/raphaelgiovanini/memcache-top/master/memcache-top
   chmod +x memcache-top

Needs only Perl 5.10+ (present on almost every Linux and macOS box).

USAGE
-----

::

   ./memcache-top --instances 127.0.0.1           # --instances is required
   ./memcache-top --instances mc1,mc2:11212 --sleep 5
   ./memcache-top --instances mc1 --bytes         # add RX/s and TX/s columns
   ./memcache-top --instances mc1 --lang pt       # Portuguese interface
   ./memcache-top --instances mc1 --oneoff        # exit 0 OK, 1 WARN, 2 CRIT, 3 bad usage

   - ``--instances h:p,...``  instances to watch (required; repeat or comma separate)
   - ``--port N``             default port when an instance has none (11211)
   - ``--sleep N``            refresh interval in seconds (3), or as a bare number
   - ``--lang en|pt|es``      interface language (default: from LANG, else en)
   - ``--color / --nocolor``  colored output (on)
   - ``--lifetime``           stats averaged over server uptime
   - ``--bytes / --nobytes``  read and write bytes columns (off)
   - ``--commands / --nocommands``  get and set columns (on)
   - ``--cumulative``         totals since memcache-top started
   - ``--oneoff``             print once and exit, for scripts and monitoring
     checks (cron, Nagios, Zabbix)

WHAT IT FLAGS
-------------

   - CRIT: instance unreachable
   - CRIT: rejecting connections (max_connections reached)
   - WARN/CRIT: connections near max_connections
   - WARN/CRIT: evictions, shown with how full memory is
   - WARN/CRIT: low hit ratio, only above 10 gets/s so idle instances
     don't cause noise
   - WARN: recently restarted, cache is cold
   - WARN/CRIT: slow 'stats' round-trip

   A full cache alone is not flagged: memcached is meant to fill up and
   evict by LRU.  Evictions are what tell you it is too small.

   The Mem and Con bars take the color of the worst instance, so one
   overloaded node is not hidden by a healthy cluster average.

   Hit ratio and rates are per refresh interval, measured on a persistent
   connection.  The first screen shows ``-`` until there are two samples.

THRESHOLDS
----------

   Edit %limit at the top of the script.  Each metric has a warning
   (yellow) and critical (red) level::

      evictions => [1, 50],      # evictions per second
      hit_ratio => [80, 50],     # % of gets that hit
      conn_pct  => [80, 95],     # curr_connections as % of max_connections
      latency   => [50, 250],    # ms for one 'stats' round-trip
      mem       => [90, 98],     # % of limit_maxbytes; color only

   Watching an instance over a WAN?  Raise ``latency`` above your network
   round-trip, or it will always show yellow or red.

TRANSLATIONS
------------

   All messages live in ``%msg`` near the top of the script.  To add a
   language, copy the ``en`` block, translate it and send a pull request.
   Missing keys fall back to English.

AUTHORS
-------

   - Raphael Giovanini - maintainer; v0.8+ redesign, alerts, translations
   - Nicholas Tang - original author (2009)
   - Contributors: Evan Culver, richlv and others, see the git history
