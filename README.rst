# memcache-top.pl

"top" for memcache - watch the traffic and other stats in real-time.  Yoikes.

# NOTES:

   If Getopt::Long is installed:
     - Specify instances w/ --instances (multiple times or comma separated)
     - Specify default port w/ --port (defaults to 11211)
     - Specify sleep time w/ --sleep (default 3)
     - Specify color output w/ --color (default) or --nocolor
     - Specify lifetime stats w/ --lifetime or --nolifetime (default)
       NOTE: lifetime stats break thresholds for evictions, bytes.
     - Specify read and write bytes w/ --bytes (default) or --nobytes
     - Specify get and set commands w/ --commands or --nocommands (default)
     - Specify cumulative numbers w/ --cumulative (don't use with lifetime)
     - Run a single time without clearing the screen, good for scripts and
       the like: --oneoff

   If Getopt::Long is not installed:
     - Specify sleep time by typing a number after the command.
   Specify instances in @default_instances.
   Specify thresholds by defining %threshold.
   Written against memcached v 1.2.3, but works fine w/ later versions.
