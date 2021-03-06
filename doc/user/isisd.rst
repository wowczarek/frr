.. _isis:

****
ISIS
****

:abbr:`ISIS (Intermediate System to Intermediate System)` is a routing protocol
which is described in :t:`ISO10589`, :rfc:`1195`, :rfc:`5308`. ISIS is an
:abbr:`IGP (Interior Gateway Protocol)`. Compared with :abbr:`RIP`,
:abbr:`ISIS` can provide scalable network support and faster convergence times
like :abbr:`OSPF`. ISIS is widely used in large networks such as :abbr:`ISP
(Internet Service Provider)` and carrier backbone networks.

.. _configuring-isisd:

Configuring isisd
=================

There are no *isisd* specific options. Common options can be specified
(:ref:`common-invocation-options`) to *isisd*. *isisd* needs to acquire
interface information from *zebra* in order to function. Therefore *zebra* must
be running before invoking *isisd*. Also, if *zebra* is restarted then *isisd*
must be too.

Like other daemons, *isisd* configuration is done in :abbr:`ISIS` specific
configuration file :file:`isisd.conf`.

.. _isis-router:

ISIS router
===========

To start the ISIS process you have to specify the ISIS router. As of this
writing, *isisd* does not support multiple ISIS processes.

.. index:: router isis WORD [vrf NAME]
.. clicmd:: [no] router isis WORD [vrf NAME]

   Enable or disable the ISIS process by specifying the ISIS domain with
   'WORD'.  *isisd* does not yet support multiple ISIS processes but you must
   specify the name of ISIS process. The ISIS process name 'WORD' is then used
   for interface (see command :clicmd:`ip router isis WORD`).

.. index:: net XX.XXXX. ... .XXX.XX
.. clicmd:: net XX.XXXX. ... .XXX.XX

.. index:: net XX.XXXX. ... .XXX.XX
.. clicmd:: no net XX.XXXX. ... .XXX.XX

   Set/Unset network entity title (NET) provided in ISO format.

.. index:: hostname dynamic
.. clicmd:: hostname dynamic

.. index:: hostname dynamic
.. clicmd:: no hostname dynamic

   Enable support for dynamic hostname.

.. index:: area-password [clear | md5] <password>
.. clicmd:: area-password [clear | md5] <password>

.. index:: domain-password [clear | md5] <password>
.. clicmd:: domain-password [clear | md5] <password>

.. index:: area-password
.. clicmd:: no area-password

.. index:: domain-password
.. clicmd:: no domain-password

   Configure the authentication password for an area, respectively a domain, as
   clear text or md5 one.

.. index:: attached-bit [receive ignore | send]
.. clicmd:: attached-bit [receive ignore | send]

.. index:: attached-bit
.. clicmd:: no attached-bit

   Set attached bit for inter-area traffic:

   - receive
     If LSP received with attached bit set, create default route to neighbor
   - send
     If L1|L2 router, set attached bit in LSP sent to L1 router

.. index:: log-adjacency-changes
.. clicmd:: log-adjacency-changes

.. index:: log-adjacency-changes
.. clicmd:: no log-adjacency-changes

   Log changes in adjacency state.

.. index:: metric-style [narrow | transition | wide]
.. clicmd:: metric-style [narrow | transition | wide]

.. index:: metric-style
.. clicmd:: no metric-style

   Set old-style (ISO 10589) or new-style packet formats:

   - narrow
     Use old style of TLVs with narrow metric
   - transition
     Send and accept both styles of TLVs during transition
   - wide
     Use new style of TLVs to carry wider metric

.. index:: set-overload-bit
.. clicmd:: set-overload-bit

.. index:: set-overload-bit
.. clicmd:: no set-overload-bit

   Set overload bit to avoid any transit traffic.

.. index:: purge-originator
.. clicmd:: purge-originator

.. index:: purge-originator
.. clicmd:: no purge-originator

   Enable or disable :rfc:`6232` purge originator identification.

.. index:: lsp-mtu (128-4352)
.. clicmd:: [no] lsp-mtu (128-4352)

   Configure the maximum size of generated LSPs, in bytes.


.. _isis-timer:

ISIS Timer
==========

.. index:: lsp-gen-interval (1-120)
.. clicmd:: lsp-gen-interval (1-120)

.. index:: lsp-gen-interval [level-1 | level-2] (1-120)
.. clicmd:: lsp-gen-interval [level-1 | level-2] (1-120)

.. index:: lsp-gen-interval
.. clicmd:: no lsp-gen-interval

.. index:: lsp-gen-interval [level-1 | level-2]
.. clicmd:: no lsp-gen-interval [level-1 | level-2]

   Set minimum interval in seconds between regenerating same LSP,
   globally, for an area (level-1) or a domain (level-2).

.. index:: lsp-refresh-interval [level-1 | level-2] (1-65235)
.. clicmd:: lsp-refresh-interval [level-1 | level-2] (1-65235)

.. index:: lsp-refresh-interval [level-1 | level-2]
.. clicmd:: no lsp-refresh-interval [level-1 | level-2]

   Set LSP refresh interval in seconds, globally, for an area (level-1) or a
   domain (level-2).

.. index:: max-lsp-lifetime (360-65535)
.. clicmd:: max-lsp-lifetime (360-65535)

.. index:: max-lsp-lifetime [level-1 | level-2] (360-65535)
.. clicmd:: max-lsp-lifetime [level-1 | level-2] (360-65535)

.. index:: max-lsp-lifetime
.. clicmd:: no max-lsp-lifetime

.. index:: max-lsp-lifetime [level-1 | level-2]
.. clicmd:: no max-lsp-lifetime [level-1 | level-2]

   Set LSP maximum LSP lifetime in seconds, globally, for an area (level-1) or
   a domain (level-2).

.. index:: spf-interval (1-120)
.. clicmd:: spf-interval (1-120)

.. index:: spf-interval [level-1 | level-2] (1-120)
.. clicmd:: spf-interval [level-1 | level-2] (1-120)

.. index:: spf-interval
.. clicmd:: no spf-interval

.. index:: spf-interval [level-1 | level-2]
.. clicmd:: no spf-interval [level-1 | level-2]

   Set minimum interval between consecutive SPF calculations in seconds.

.. _isis-fast-reroute:

ISIS Fast-Reroute
=================

.. index:: spf prefix-priority [critical | high | medium] WORD
.. clicmd:: spf prefix-priority [critical | high | medium] WORD

.. index:: spf prefix-priority [critical | high | medium] WORD
.. clicmd:: no spf prefix-priority [critical | high | medium] [WORD]

   Assign a priority to the prefixes that match the specified access-list.

.. index:: fast-reroute priority-limit [critical | high | medium] [level-1 | level-2]
.. clicmd:: [no] fast-reroute priority-limit [critical | high | medium] [level-1 | level-2]

   Limit LFA backup computation up to the specified prefix priority.

.. index:: fast-reroute lfa tiebreaker [downstream | lowest-backup-metric | node-protecting] index (1-255) [level-1 | level-2]
.. clicmd:: [no] fast-reroute lfa tiebreaker [downstream | lowest-backup-metric | node-protecting] index (1-255) [level-1 | level-2]

   Configure a tie-breaker for multiple LFA backups. Lower indexes are processed
   first.

.. index:: fast-reroute load-sharing disable [level-1 | level-2]
.. clicmd:: [no] fast-reroute load-sharing disable [level-1 | level-2]

   Disable load sharing across multiple LFA backups.

.. index:: fast-reroute remote-lfa prefix-list WORD [level-1 | level-2]
.. clicmd:: [no] fast-reroute remote-lfa prefix-list [WORD] [level-1 | level-2]

   Configure a prefix-list to select eligible PQ nodes (valid for all protected
   interfaces).

.. _isis-region:

ISIS region
===========

.. index:: is-type [level-1 | level-1-2 | level-2-only]
.. clicmd:: is-type [level-1 | level-1-2 | level-2-only]

.. index:: is-type
.. clicmd:: no is-type

   Define the ISIS router behavior:

   - level-1
     Act as a station router only
   - level-1-2
     Act as both a station router and an area router
   - level-2-only
     Act as an area router only

.. _isis-interface:

ISIS interface
==============

.. _ip-router-isis-word:

.. index:: ip router isis WORD [vrf NAME]
.. index:: ipv6 router isis WORD [vrf NAME]
.. clicmd:: [no] <ip|ipv6> router isis WORD [vrf NAME]

   Activate ISIS adjacency on this interface. Note that the name of ISIS
   instance must be the same as the one used to configure the ISIS process (see
   command :clicmd:`router isis WORD`). To enable IPv4, issue ``ip router isis
   WORD``; to enable IPv6, issue ``ipv6 router isis WORD``.

.. index:: isis circuit-type [level-1 | level-1-2 | level-2]
.. clicmd:: isis circuit-type [level-1 | level-1-2 | level-2]

.. index:: isis circuit-type
.. clicmd:: no isis circuit-type

   Configure circuit type for interface:

   - level-1
     Level-1 only adjacencies are formed
   - level-1-2
     Level-1-2 adjacencies are formed
   - level-2-only
     Level-2 only adjacencies are formed

.. index:: isis csnp-interval (1-600)
.. clicmd:: isis csnp-interval (1-600)

.. index:: isis csnp-interval (1-600) [level-1 | level-2]
.. clicmd:: isis csnp-interval (1-600) [level-1 | level-2]

.. index:: isis csnp-interval
.. clicmd:: no isis csnp-interval

.. index:: isis csnp-interval [level-1 | level-2]
.. clicmd:: no isis csnp-interval [level-1 | level-2]

   Set CSNP interval in seconds globally, for an area (level-1) or a domain
   (level-2).

.. index:: isis hello padding
.. clicmd:: isis hello padding

   Add padding to IS-IS hello packets.

.. index:: isis hello-interval (1-600)
.. clicmd:: isis hello-interval (1-600)

.. index:: isis hello-interval (1-600) [level-1 | level-2]
.. clicmd:: isis hello-interval (1-600) [level-1 | level-2]

.. index:: isis hello-interval
.. clicmd:: no isis hello-interval

.. index:: isis hello-interval [level-1 | level-2]
.. clicmd:: no isis hello-interval [level-1 | level-2]

   Set Hello interval in seconds globally, for an area (level-1) or a domain
   (level-2).

.. index:: isis hello-multiplier (2-100)
.. clicmd:: isis hello-multiplier (2-100)

.. index:: isis hello-multiplier (2-100) [level-1 | level-2]
.. clicmd:: isis hello-multiplier (2-100) [level-1 | level-2]

.. index:: isis hello-multiplier
.. clicmd:: no isis hello-multiplier

.. index:: isis hello-multiplier [level-1 | level-2]
.. clicmd:: no isis hello-multiplier [level-1 | level-2]

   Set multiplier for Hello holding time globally, for an area (level-1) or a
   domain (level-2).

.. index:: isis metric [(0-255) | (0-16777215)]
.. clicmd:: isis metric [(0-255) | (0-16777215)]

.. index:: isis metric [(0-255) | (0-16777215)] [level-1 | level-2]
.. clicmd:: isis metric [(0-255) | (0-16777215)] [level-1 | level-2]

.. index:: isis metric
.. clicmd:: no isis metric

.. index:: isis metric [level-1 | level-2]
.. clicmd:: no isis metric [level-1 | level-2]

   Set default metric value globally, for an area (level-1) or a domain
   (level-2).  Max value depend if metric support narrow or wide value (see
   command :clicmd:`metric-style [narrow | transition | wide]`).

.. index:: isis network point-to-point
.. clicmd:: isis network point-to-point

.. index:: isis network point-to-point
.. clicmd:: no isis network point-to-point

   Set network type to 'Point-to-Point' (broadcast by default).

.. index:: isis passive
.. clicmd:: isis passive

.. index:: isis passive
.. clicmd:: no isis passive

   Configure the passive mode for this interface.

.. index:: isis password [clear | md5] <password>
.. clicmd:: isis password [clear | md5] <password>

.. index:: isis password
.. clicmd:: no isis password

   Configure the authentication password (clear or encoded text) for the
   interface.

.. index:: isis priority (0-127)
.. clicmd:: isis priority (0-127)

.. index:: isis priority (0-127) [level-1 | level-2]
.. clicmd:: isis priority (0-127) [level-1 | level-2]

.. index:: isis priority
.. clicmd:: no isis priority

.. index:: isis priority [level-1 | level-2]
.. clicmd:: no isis priority [level-1 | level-2]

   Set priority for Designated Router election, globally, for the area
   (level-1) or the domain (level-2).

.. index:: isis psnp-interval (1-120)
.. clicmd:: isis psnp-interval (1-120)

.. index:: isis psnp-interval (1-120) [level-1 | level-2]
.. clicmd:: isis psnp-interval (1-120) [level-1 | level-2]

.. index:: isis psnp-interval
.. clicmd:: no isis psnp-interval

.. index:: isis psnp-interval [level-1 | level-2]
.. clicmd:: no isis psnp-interval [level-1 | level-2]

   Set PSNP interval in seconds globally, for an area (level-1) or a domain
   (level-2).

.. index:: isis three-way-handshake
.. clicmd:: isis three-way-handshake

.. index:: isis three-way-handshake
.. clicmd:: no isis three-way-handshake

   Enable or disable :rfc:`5303` Three-Way Handshake for P2P adjacencies.
   Three-Way Handshake is enabled by default.

.. index:: isis fast-reroute lfa [level-1 | level-2]
.. clicmd:: [no] isis fast-reroute lfa [level-1 | level-2]

   Enable per-prefix LFA fast reroute link protection.

.. index:: isis fast-reroute lfa [level-1 | level-2] exclude interface IFNAME
.. clicmd:: [no] isis fast-reroute lfa [level-1 | level-2] exclude interface IFNAME

   Exclude an interface from the LFA backup nexthop computation.

.. index:: isis fast-reroute ti-lfa [level-1|level-2] [node-protection]
.. clicmd:: [no] isis fast-reroute ti-lfa [level-1|level-2] [node-protection]

   Enable per-prefix TI-LFA fast reroute link or node protection.

.. index:: isis fast-reroute remote-lfa tunnel mpls-ldp [level-1 | level-2]
.. clicmd:: [no] isis fast-reroute remote-lfa tunnel mpls-ldp [level-1 | level-2]

   Enable per-prefix Remote LFA fast reroute link protection. Note that other
   routers in the network need to be configured to accept LDP targeted hello
   messages in order for RLFA to work.

.. index:: isis fast-reroute remote-lfa maximum-metric (1-16777215) [level-1 | level-2]
.. clicmd:: [no] isis fast-reroute remote-lfa maximum-metric (1-16777215) [level-1 | level-2]

   Limit Remote LFA PQ node selection within the specified metric.

.. _showing-isis-information:

Showing ISIS information
========================

.. index:: show isis summary
.. clicmd:: show isis summary

   Show summary information about ISIS.

.. index:: show isis hostname
.. clicmd:: show isis hostname

   Show information about ISIS node.

.. index:: show isis interface
.. clicmd:: show isis interface

.. index:: show isis interface detail
.. clicmd:: show isis interface detail

.. index:: show isis interface <interface name>
.. clicmd:: show isis interface <interface name>

   Show state and configuration of ISIS specified interface, or all interfaces
   if no interface is given with or without details.

.. index:: show isis neighbor
.. clicmd:: show isis neighbor

.. index:: show isis neighbor <System Id>
.. clicmd:: show isis neighbor <System Id>

.. index:: show isis neighbor detail
.. clicmd:: show isis neighbor detail

   Show state and information of ISIS specified neighbor, or all neighbors if
   no system id is given with or without details.

.. index:: show isis database
.. clicmd:: show isis database

.. index:: show isis database [detail]
.. clicmd:: show isis database [detail]

.. index:: show isis database <LSP id> [detail]
.. clicmd:: show isis database <LSP id> [detail]

.. index:: show isis database detail <LSP id>
.. clicmd:: show isis database detail <LSP id>

   Show the ISIS database globally, for a specific LSP id without or with
   details.

.. index:: show isis topology
.. clicmd:: show isis topology

.. index:: show isis topology [level-1|level-2]
.. clicmd:: show isis topology [level-1|level-2]

   Show topology IS-IS paths to Intermediate Systems, globally, in area
   (level-1) or domain (level-2).

.. index:: show isis route [level-1|level-2] [prefix-sid|backup]
.. clicmd:: show isis route [level-1|level-2] [prefix-sid|backup]

   Show the ISIS routing table, as determined by the most recent SPF
   calculation.

.. index:: show isis fast-reroute summary [level-1|level-2]
.. clicmd:: show isis fast-reroute summary [level-1|level-2]

   Show information about the number of prefixes having LFA protection,
   and network-wide LFA coverage.

.. _isis-traffic-engineering:

Traffic Engineering
===================

.. note::

   At this time, FRR offers partial support for some of the routing
   protocol extensions that can be used with MPLS-TE. FRR does not
   support a complete RSVP-TE solution currently.

.. index:: mpls-te on
.. clicmd:: mpls-te on

.. index:: mpls-te
.. clicmd:: no mpls-te

   Enable Traffic Engineering LSP flooding.

.. index:: mpls-te router-address <A.B.C.D>
.. clicmd:: mpls-te router-address <A.B.C.D>

.. index:: mpls-te router-address
.. clicmd:: no mpls-te router-address

   Configure stable IP address for MPLS-TE.

.. index:: show isis mpls-te interface
.. clicmd:: show isis mpls-te interface

.. index:: show isis mpls-te interface INTERFACE
.. clicmd:: show isis mpls-te interface INTERFACE

   Show MPLS Traffic Engineering parameters for all or specified interface.

.. index:: show isis mpls-te router
.. clicmd:: show isis mpls-te router

   Show Traffic Engineering router parameters.

.. seealso::

   :ref:`ospf-traffic-engineering`

.. _debugging-isis:

Segment Routing
===============

This is an EXPERIMENTAL support of Segment Routing as per RFC8667
for MPLS dataplane. It supports IPv4, IPv6 and ECMP and has been
tested against Cisco & Juniper routers.

Known limitations:
 - No support for level redistribution (L1 to L2 or L2 to L1)
 - No support for binding SID
 - No support for SRMS
 - No support for SRLB
 - Only one SRGB and default SPF Algorithm is supported

.. index:: segment-routing on
.. clicmd:: [no] segment-routing on

   Enable Segment Routing.

.. index:: segment-routing global-block (0-1048575) (0-1048575)
.. clicmd:: [no] segment-routing global-block (0-1048575) (0-1048575)

   Set the Segment Routing Global Block i.e. the label range used by MPLS
   to store label in the MPLS FIB for Prefix SID. Note that the block size
   may not exceed 65535.

.. index:: segment-routing local-block (0-1048575) (0-1048575)
.. clicmd:: [no] segment-routing local-block (0-1048575) (0-1048575)

   Set the Segment Routing Local Block i.e. the label range used by MPLS
   to store label in the MPLS FIB for Adjacency SID. Note that the block size
   may not exceed 65535.

.. index:: segment-routing node-msd (1-16)
.. clicmd:: [no] segment-routing node-msd (1-16)

   Set the Maximum Stack Depth supported by the router. The value depend of the
   MPLS dataplane. E.g. for Linux kernel, since version 4.13 the maximum value
   is 32.

.. index:: segment-routing prefix <A.B.C.D/M|X:X::X:X/M> <absolute (16-1048575)|index (0-65535)> [no-php-flag|explicit-null] [n-flag-clear]
.. clicmd:: [no] segment-routing prefix <A.B.C.D/M|X:X::X:X/M> <absolute (16-1048575)|index (0-65535) [no-php-flag|explicit-null] [n-flag-clear]

   Set the Segment Routing index or absolute label value for the specified
   prefix. The 'no-php-flag' means NO Penultimate Hop Popping that allows SR
   node to request to its neighbor to not pop the label. The 'explicit-null'
   flag allows SR node to request to its neighbor to send IP packet with the
   EXPLICIT-NULL label. The 'n-flag-clear' option can be used to explicitly
   clear the Node flag that is set by default for Prefix-SIDs associated to
   loopback addresses. This option is necessary to configure Anycast-SIDs.

.. index:: show isis segment-routing prefix-sids
.. clicmd:: show isis segment-routing prefix-sids

   Show detailed information about all learned Segment Routing Prefix-SIDs.

.. index:: show isis segment-routing nodes
.. clicmd:: show isis segment-routing nodes

   Show detailed information about all learned Segment Routing Nodes.

Debugging ISIS
==============

.. index:: debug isis adj-packets
.. clicmd:: debug isis adj-packets

.. index:: debug isis adj-packets
.. clicmd:: no debug isis adj-packets

   IS-IS Adjacency related packets.

.. index:: debug isis checksum-errors
.. clicmd:: debug isis checksum-errors

.. index:: debug isis checksum-errors
.. clicmd:: no debug isis checksum-errors

   IS-IS LSP checksum errors.

.. index:: debug isis events
.. clicmd:: debug isis events

.. index:: debug isis events
.. clicmd:: no debug isis events

   IS-IS Events.

.. index:: debug isis local-updates
.. clicmd:: debug isis local-updates

.. index:: debug isis local-updates
.. clicmd:: no debug isis local-updates

   IS-IS local update packets.

.. index:: debug isis packet-dump
.. clicmd:: debug isis packet-dump

.. index:: debug isis packet-dump
.. clicmd:: no debug isis packet-dump

   IS-IS packet dump.

.. index:: debug isis protocol-errors
.. clicmd:: debug isis protocol-errors

.. index:: debug isis protocol-errors
.. clicmd:: no debug isis protocol-errors

   IS-IS LSP protocol errors.

.. index:: debug isis route-events
.. clicmd:: debug isis route-events

.. index:: debug isis route-events
.. clicmd:: no debug isis route-events

   IS-IS Route related events.

.. index:: debug isis snp-packets
.. clicmd:: debug isis snp-packets

.. index:: debug isis snp-packets
.. clicmd:: no debug isis snp-packets

   IS-IS CSNP/PSNP packets.

.. index:: debug isis spf-events
.. clicmd:: debug isis spf-events

.. index:: debug isis spf-statistics
.. clicmd:: debug isis spf-statistics

.. index:: debug isis spf-triggers
.. clicmd:: debug isis spf-triggers

.. index:: debug isis spf-events
.. clicmd:: no debug isis spf-events

.. index:: debug isis spf-statistics
.. clicmd:: no debug isis spf-statistics

.. index:: debug isis spf-triggers
.. clicmd:: no debug isis spf-triggers

   IS-IS Shortest Path First Events, Timing and Statistic Data and triggering
   events.

.. index:: debug isis update-packets
.. clicmd:: debug isis update-packets

.. index:: debug isis update-packets
.. clicmd:: no debug isis update-packets

   Update related packets.

.. index:: debug isis sr-events
.. clicmd:: debug isis sr-events

.. index:: debug isis sr-events
.. clicmd:: no debug isis sr-events

   IS-IS Segment Routing events.

.. index:: debug isis lfa
.. clicmd:: debug isis lfa

.. index:: debug isis lfa
.. clicmd:: no debug isis lfa

   IS-IS LFA events.

.. index:: show debugging isis
.. clicmd:: show debugging isis

   Print which ISIS debug level is activate.

ISIS Configuration Examples
===========================

A simple example, with MD5 authentication enabled:

.. code-block:: frr

   !
   interface eth0
    ip router isis FOO
    isis network point-to-point
    isis circuit-type level-2-only
   !
   router isis FOO
   net 47.0023.0000.0000.0000.0000.0000.0000.1900.0004.00
    metric-style wide
    is-type level-2-only


A Traffic Engineering configuration, with Inter-ASv2 support.

First, the :file:`zebra.conf` part:

.. code-block:: frr

   hostname HOSTNAME
   password PASSWORD
   log file /var/log/zebra.log
   !
   interface eth0
    ip address 10.2.2.2/24
    link-params
     max-bw 1.25e+07
     max-rsv-bw 1.25e+06
     unrsv-bw 0 1.25e+06
     unrsv-bw 1 1.25e+06
     unrsv-bw 2 1.25e+06
     unrsv-bw 3 1.25e+06
     unrsv-bw 4 1.25e+06
     unrsv-bw 5 1.25e+06
     unrsv-bw 6 1.25e+06
     unrsv-bw 7 1.25e+06
     admin-grp 0xab
   !
   interface eth1
    ip address 10.1.1.1/24
    link-params
     enable
     metric 100
     max-bw 1.25e+07
     max-rsv-bw 1.25e+06
     unrsv-bw 0 1.25e+06
     unrsv-bw 1 1.25e+06
     unrsv-bw 2 1.25e+06
     unrsv-bw 3 1.25e+06
     unrsv-bw 4 1.25e+06
     unrsv-bw 5 1.25e+06
     unrsv-bw 6 1.25e+06
     unrsv-bw 7 1.25e+06
     neighbor 10.1.1.2 as 65000


Then the :file:`isisd.conf` itself:

.. code-block:: frr

   hostname HOSTNAME
   password PASSWORD
   log file /var/log/isisd.log
   !
   !
   interface eth0
    ip router isis FOO
   !
   interface eth1
    ip router isis FOO
   !
   !
   router isis FOO
    isis net 47.0023.0000.0000.0000.0000.0000.0000.1900.0004.00
     mpls-te on
     mpls-te router-address 10.1.1.1
   !
   line vty

A Segment Routing configuration, with IPv4, IPv6, SRGB and MSD configuration.

.. code-block:: frr

   hostname HOSTNAME
   password PASSWORD
   log file /var/log/isisd.log
   !
   !
   interface eth0
    ip router isis SR
    isis network point-to-point
   !
   interface eth1
    ip router isis SR
   !
   !
   router isis SR
    net 49.0000.0000.0000.0001.00
    is-type level-1
    topology ipv6-unicast
    lsp-gen-interval 2
    segment-routing on
    segment-routing node-msd 8
    segment-routing prefix 10.1.1.1/32 index 100 explicit-null
    segment-routing prefix 2001:db8:1000::1/128 index 101 explicit-null
   !

ISIS Vrf Configuration Examples
===============================

A simple vrf example:

.. code-block:: frr

   !
   interface eth0 vrf RED
    ip router isis FOO vrf RED
    isis network point-to-point
    isis circuit-type level-2-only
   !
   router isis FOO vrf RED
    net 47.0023.0000.0000.0000.0000.0000.0000.1900.0004.00
    metric-style wide
    is-type level-2-only


