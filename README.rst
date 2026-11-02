ESPixelStick copy
-----------------

This is the ESP8266mDNS library as shipped in esp8266/Arduino core 3.1.2 (LEAmDNS, version 1.2), carried
as a separate library so that it can be fixed ahead of the core. PlatformIO picks a ``lib_deps`` library over
a framework library of the same name, so pinning this repository from ``platformio.ini`` replaces the
core's copy in the build.

Changes against the core (see the git history):

- A received message is parsed only while a heap block of ``MDNS_MIN_FREE_BLOCK`` bytes (2048 unless
  overridden) is free; otherwise it is dropped unread. The core's responder allocates every record with a
  plain ``new`` and the ESP8266 build has no exceptions, so a message that arrives while the heap is short
  resets the board.
- The allocations of the responder use ``new (std::nothrow)`` where the result is checked, and the six
  record readers in ``_readRRAnswer()`` check theirs.

Everything else is unchanged, including the license of the original files.

ESP8266 Multicast DNS
=====================

A port of CC3000 Multicast DNS library (version 1.1)

This is a simple implementation of multicast DNS query support for an
Arduino running on ESP8266 chip. Only support for resolving address
queries is currently implemented.

Requirements
------------

-  ESP8266WiFi library
-  MDNS support in your operating system/client machines:
-  For Mac OSX support is built in through Bonjour already.
-  For Linux, install `Avahi <http://avahi.org/>`__.
-  For Windows, install
   `Bonjour <http://www.apple.com/support/bonjour/>`__.

Usage
-----

1. Download this repository as a zip (button on the right) and follow
   `these instructions to install into
   Arduino <http://arduino.cc/en/Guide/Libraries>`__.
2. Include the ESP8266mDNS library in the sketch.
3. Call MDNS.begin method in the sketch's setup and provide a domain
   name (without the '.local' suffix, i.e. just provide 'foo' to resolve
   'foo.local'). Optionally provide the IP address to advertise and time
   to live (in seconds) for the DNS record -- the default is 1 hour.
4. To advertise DNS-SD services, call MDNS.addService(service, proto,
   port), where service and proto are strings with service and protocol
   name (e.g. "http", "tcp"), and port is an integer port number for
   this service (e.g. 80).

See the included MDNS + HTTP server sketch for a full example.

License
-------

Copyright (c) 2013 Tony DiCola (tony@tonydicola.com) ESP8266 port (c)
2015 Ivan Grokhotkov (ivan@esp8266.com)

Permission is hereby granted, free of charge, to any person obtaining a
copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be included
in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS
OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
