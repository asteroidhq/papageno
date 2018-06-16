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
 - Strips inbound rogue BGP communities
 - Tags every peering route with 
    - the PeeringDB IX ID it was learned at
    - The ISO Country ID it was learned in
    - The region it was learned in
 - Tags every filtered route with a Large BGP community to indicate why it was filtered
 - Honors graceful shutdown

Standard export filters include:
 - IPv4 and IPv6 'martian' prefixes - networks that aren't supposed to be on the Internet
 - Strips private ASNs for external peers
 - Strips local BGP communities
 - Checks on your own prefixes

Predefined filter sets for sessions with:
 - Transit providers
 - Peers on an IXP or private interconnect
 - Route servers on an IXP
 - Customer connections
 - Internal BGP sessions
 
It also configures Bird to be compatible with birdseye, a bird-based looking glass tool. 
There are separate commands for updating peering sessions, updating IRR filters and syncing with peeringdb so updates can be done independently (and automated!).

# Requirements
 - Bird 1.6
 - Perl 5 or later
    The following non-standard modules:
    - LWP::Simple (libwww-perl)
    - JSON (libjson-perl)
 - bgpq3

# Usage
 - edit envvars to the correct settings 
 - edit bird.conf and bird6.conf to reflect your asn and prefixes
 - edit bgp-peers.csv to configure your BGP peers
 - After every edit, do ./run_papageno peers'
 - Periodically (a few times a day) do './run_papageno filters' to update AS-SET filters
 - Run './run_papageno peeringdb' every time you connect to a new IX
 - Optional but highly recommended:
    - edit papageno-cron.d.sample for your configuration and copy to /etc/cron.d to automate periodic updates
    - edit sudoers.sample and add to /etc/sudoers
    - add iptables.conf.sample and ip6tables.conf.sample to your iptables configuration and enable update-iptables in envvars 

Happy peering!

