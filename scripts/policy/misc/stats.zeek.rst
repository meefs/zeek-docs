:tocdepth: 3

policy/misc/stats.zeek
======================
.. zeek:namespace:: Stats

Log memory/packet/lag statistics.

:Namespace: Stats
:Imports: :doc:`base/frameworks/notice </scripts/base/frameworks/notice/index>`, :doc:`base/frameworks/telemetry </scripts/base/frameworks/telemetry/index>`, :doc:`base/utils/time.zeek </scripts/base/utils/time.zeek>`

Summary
~~~~~~~
Runtime Options
###############
============================================================================ =============================
:zeek:id:`Stats::report_interval`: :zeek:type:`interval` :zeek:attr:`&redef` How often stats are reported.
============================================================================ =============================

Types
#####
============================================= =
:zeek:type:`Stats::Info`: :zeek:type:`record` 
============================================= =

Redefinitions
#############
======================================= =========================
:zeek:type:`Log::ID`: :zeek:type:`enum` 
                                        
                                        * :zeek:enum:`Stats::LOG`
======================================= =========================

Events
######
=============================================== ===============================================================
:zeek:id:`Stats::log_stats`: :zeek:type:`event` Event to catch stats as they are written to the logging stream.
=============================================== ===============================================================

Hooks
#####
========================================================== =
:zeek:id:`Stats::log_policy`: :zeek:type:`Log::PolicyHook` 
========================================================== =


Detailed Interface
~~~~~~~~~~~~~~~~~~
Runtime Options
###############
.. zeek:id:: Stats::report_interval
   :source-code: policy/misc/stats.zeek 15 15

   :Type: :zeek:type:`interval`
   :Attributes: :zeek:attr:`&redef`
   :Default: ``5.0 mins``

   How often stats are reported.

Types
#####
.. zeek:type:: Stats::Info
   :source-code: policy/misc/stats.zeek 17 86

   :Type: :zeek:type:`record`


   .. zeek:field:: ts :zeek:type:`time` :zeek:attr:`&log`

      Timestamp for the measurement.


   .. zeek:field:: peer :zeek:type:`string` :zeek:attr:`&log`

      Peer that generated this log.  Mostly for clusters.


   .. zeek:field:: mem :zeek:type:`count` :zeek:attr:`&log`

      Amount of memory currently in use in MB.


   .. zeek:field:: pkts_proc :zeek:type:`count` :zeek:attr:`&log`

      Number of packets processed since the last stats interval.


   .. zeek:field:: bytes_recv :zeek:type:`count` :zeek:attr:`&log`

      Number of bytes received since the last stats interval if
      reading live traffic.


   .. zeek:field:: pkts_dropped :zeek:type:`count` :zeek:attr:`&log` :zeek:attr:`&optional`

      Number of packets dropped since the last stats interval if
      reading live traffic.


   .. zeek:field:: pkts_link :zeek:type:`count` :zeek:attr:`&log` :zeek:attr:`&optional`

      Number of packets seen on the link since the last stats
      interval if reading live traffic.


   .. zeek:field:: pkt_lag :zeek:type:`interval` :zeek:attr:`&log` :zeek:attr:`&optional`

      Lag between the wall clock and packet timestamps if reading
      live traffic.


   .. zeek:field:: pkts_filtered :zeek:type:`count` :zeek:attr:`&log` :zeek:attr:`&optional`

      Number of packets filtered from the link since the last
      stats interval if reading live traffic.


   .. zeek:field:: events_proc :zeek:type:`count` :zeek:attr:`&log`

      Number of events processed since the last stats interval.


   .. zeek:field:: events_queued :zeek:type:`count` :zeek:attr:`&log`

      Number of events that have been queued since the last stats
      interval.


   .. zeek:field:: active_tcp_conns :zeek:type:`count` :zeek:attr:`&log`

      TCP connections currently in memory.


   .. zeek:field:: active_udp_conns :zeek:type:`count` :zeek:attr:`&log`

      UDP connections currently in memory.


   .. zeek:field:: active_icmp_conns :zeek:type:`count` :zeek:attr:`&log`

      ICMP connections currently in memory.


   .. zeek:field:: tcp_conns :zeek:type:`count` :zeek:attr:`&log`

      TCP connections seen since last stats interval.


   .. zeek:field:: udp_conns :zeek:type:`count` :zeek:attr:`&log`

      UDP connections seen since last stats interval.


   .. zeek:field:: icmp_conns :zeek:type:`count` :zeek:attr:`&log`

      ICMP connections seen since last stats interval.


   .. zeek:field:: timers :zeek:type:`count` :zeek:attr:`&log`

      Number of timers scheduled since last stats interval.


   .. zeek:field:: active_timers :zeek:type:`count` :zeek:attr:`&log`

      Current number of scheduled timers.


   .. zeek:field:: files :zeek:type:`count` :zeek:attr:`&log`

      Number of files seen since last stats interval.


   .. zeek:field:: active_files :zeek:type:`count` :zeek:attr:`&log`

      Current number of files actively being seen.


   .. zeek:field:: dns_requests :zeek:type:`count` :zeek:attr:`&log`

      Number of DNS requests seen since last stats interval.


   .. zeek:field:: active_dns_requests :zeek:type:`count` :zeek:attr:`&log`

      Current number of DNS requests awaiting a reply.


   .. zeek:field:: reassem_tcp_size :zeek:type:`count` :zeek:attr:`&log`

      Current size of TCP data in reassembly.


   .. zeek:field:: reassem_file_size :zeek:type:`count` :zeek:attr:`&log`

      Current size of File data in reassembly.


   .. zeek:field:: reassem_frag_size :zeek:type:`count` :zeek:attr:`&log`

      Current size of packet fragment data in reassembly.


   .. zeek:field:: reassem_unknown_size :zeek:type:`count` :zeek:attr:`&log`

      Current size of unknown data in reassembly (this is only PIA buffer right now).



Events
######
.. zeek:id:: Stats::log_stats
   :source-code: policy/misc/stats.zeek 89 89

   :Type: :zeek:type:`event` (rec: :zeek:type:`Stats::Info`)

   Event to catch stats as they are written to the logging stream.

Hooks
#####
.. zeek:id:: Stats::log_policy
   :source-code: policy/misc/stats.zeek 12 12

   :Type: :zeek:type:`Log::PolicyHook`



