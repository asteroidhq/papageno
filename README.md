# papageno
Scripting and templates to make your Bird sing BGP.

Using Bird is easy, and if you're using it for BGP inside your serverfarm/cloud/wifi-mesh all is well and the simple sample configs are, well, simple. But in the outside world, they're a horrible, terrible idea to unleash on the DFZ.

Enter Papageno.

Papageno is a small set of scripts and templates that allows you to use a single CSV to configure all of your IPv4 and IPv6 peers and to make those peers as safe as possible.

Standard import filters include:
 - Checks on IRR prefix lists
 - IPv4 and IPv6 'martian' prefixes - networks that aren't supposed to be on the Internet
 - ASN bogons - AS numbers that are either private or reserved
 - transit ASNs - AS numbers of well known transit providers 
 - Checks on next-hop ASN
 - Checks on your own prefixes
 - Checks on BGP path length
 - Honors graceful shutdown

Standard export filters include:
 - IPv4 and IPv6 'martian' prefixes - networks that aren't supposed to be on the Internet
 - Checks on your own prefixes

Predefined filter sets for sessions with:
 - Transit providers
 - Peers on an IXP or provate interconnect
 - Route servers on an IXP
 - Internal BGP sessions
 
It also configures Bird to be compatible with birdseye, a bird-based looking glass tool. There are two separate tools for updating peering sessions and updating IRR filters, so updating filters can be done independently (and automated!).

Happy peering!

