HISTORY
=======

v0.3 - 2009-04-22 - ntang
  Minor cleanups.  First release to google code:
  http://code.google.com/p/memcache-top/
v0.4 - 2009-04-23 - ntang
  Added ability to specify color, sleep time, and servers on command line.
  Also added checks for Getopt::Long and Term::ANSIColor.
  Added $default_port = "11211" and padding for short server names.  Server
  names over 23 characters inc. port will break the column lineups for now.
v0.4b - 2009-04-23 - ntang
  Added total capacity, and changed "SERVER" to "INSTANCE" to be more clear.
  Server now is the hostname, instance is hostname + port.  It will
  truncate the instance and/or server to fit inside the first column
  correctly.  (Yay!)  It'll also truncate long reads/ writes (or
  technically any number) to K or M or G if it exceeds certain limits for
  readability.
v0.5 - 2009-04-24 - ntang
  Cleaned up instances vs. servers so it's internally consistent.
  Redid printing so that now it stores it all and only refreshes/ prints when
  it has the full set of data.  Warning: major hackishness.
  Switched to per-second stats by default w/ lifetime stats available.
v0.6 - 2009-04-28 - ntang
  I lied.  One more change... the ability to specify read/write bytes, or
  get/set commands, or both.  Bear in mind if you specify both you will
  exceed the width of a standard terminal!  You've been warned.  :P
  Also, some minor display changes, etc. etc.
