📘 CentOS 7 rsyslog → Graylog (UDP) Configuration & Troubleshooting Guide
Overview

This document provides a complete guide to:

Verifying rsyslog service status

Testing local logging

Configuring remote log forwarding to Graylog

Troubleshooting delayed log delivery

Production best practices

Environment:

OS: CentOS 7 (Core)

Syslog: rsyslog

Remote Log Server: Graylog

Transport: UDP (Port 8524)

1. Verify rsyslog Service Status
1.1 Check Service Status
systemctl status rsyslog

Expected Output:

Active: active (running)

If not running:

systemctl start rsyslog
systemctl enable rsyslog
1.2 Verify Process is Running
ps -ef | grep rsyslog

Expected process:

/usr/sbin/rsyslogd -n
1.3 Check Service Enabled at Boot
systemctl is-enabled rsyslog

Expected:

enabled
2. Verify Local Logging Works
2.1 Monitor System Logs

CentOS 7 uses:

/var/log/messages

Monitor live logs:

tail -f /var/log/messages
2.2 Generate Test Log
logger "TEST LOCAL SYSLOG MESSAGE"

You should see it instantly in /var/log/messages.

If not:

Check rsyslog status

Check disk space

Validate configuration

3. Validate rsyslog Configuration

Always validate before restarting:

rsyslogd -N1

Expected output:

rsyslogd: End of config validation run. Bye.

If errors appear, fix them before restarting.

4. Configure rsyslog to Send Logs to Graylog (UDP)
4.1 Create Configuration File
vi /etc/rsyslog.d/60-graylog.conf

Add the following configuration:

action(
  type="omfwd"
  target="103.129.247.241"
  port="8524"
  protocol="udp"
  template="RSYSLOG_SyslogProtocol23Format"

  # Reliability (retry indefinitely)
  action.resumeRetryCount="-1"

  # Queue settings for near real-time forwarding
  queue.type="LinkedList"
  queue.size="10000"
  queue.dequeueBatchSize="1"
  queue.workerThreads="1"
)
4.2 Explanation of Configuration
Parameter	Description
type="omfwd"	Output module for forwarding logs
target	Graylog server IP
port	Graylog input port
protocol="udp"	Uses UDP transport
template	Uses modern Syslog protocol format
action.resumeRetryCount="-1"	Infinite retry if transmission fails
queue.type="LinkedList"	In-memory queue
queue.dequeueBatchSize="1"	Send logs one by one (minimize delay)
queue.workerThreads="1"	Single worker thread
4.3 Restart rsyslog
rsyslogd -N1
systemctl restart rsyslog
systemctl status rsyslog
5. Test Remote Logging

Send test log:

logger "TEST REMOTE SYSLOG MESSAGE at $(date)"

Verify in Graylog UI.

6. Troubleshooting 15-Minute Delay in Graylog

If logs are:

Instantly visible locally

Successfully received by Graylog

But appear ~15 minutes late in UI

Then rsyslog is NOT the issue.

The delay is likely inside Graylog or Elasticsearch.

7. Verify UDP Traffic Reaches Graylog

On Graylog server:

tcpdump -nn -i any port 8524

Then on sender:

logger "UDP TEST $(date)"

If packets appear instantly in tcpdump:

Network is fine

Sender is fine

8. Check Graylog Buffers

In Graylog Web UI:

System → Nodes → Buffer & Journal

Monitor:

Input buffer %

Process buffer %

Output buffer %

Journal size

Possible Issues
Symptom	Cause
High input buffer	Heavy log rate
High process buffer	CPU bottleneck
Growing journal	Elasticsearch slow
Output buffer high	Indexing delay
9. Check Graylog Logs

On Graylog server:

tail -f /var/log/graylog-server/server.log

Look for:

Indexer failures

Journal warnings

GC pauses

Processing errors

10. Check Elasticsearch Health

On Elasticsearch server:

curl -XGET 'http://localhost:9200/_cluster/health?pretty'

Expected:

"status" : "green"
Status	Meaning
green	Healthy
yellow	Minor issue
red	Critical issue
11. Check System Resources (Graylog Server)
top
free -m

Check for:

High CPU usage

Memory exhaustion

Swap usage

Disk I/O bottlenecks

12. Important: Timestamp vs Receive Time

Graylog may sort by:

Message timestamp

OR Receive time

If logs appear old:

Change search sorting to:

Receive time

This helps determine if delay is real or timestamp-related.

13. Why UDP Is Not Recommended in Production

UDP limitations:

No delivery guarantee

No retransmission

Packet drops under load

No encryption

No flow control

14. Recommended Production Configuration (TCP)

Strongly recommended to use TCP instead of UDP.

Graylog:

Create Syslog TCP Input

rsyslog Configuration:
action(
  type="omfwd"
  target="103.129.247.241"
  port="8524"
  protocol="tcp"
  template="RSYSLOG_SyslogProtocol23Format"

  action.resumeRetryCount="-1"

  queue.type="LinkedList"
  queue.filename="graylogqueue"
  queue.maxdiskspace="1g"
  queue.size="100000"
  queue.saveonshutdown="on"
)

Benefits:

Reliable delivery

Backpressure handling

No silent packet loss

Better performance stability

15. Common Causes of Log Delay
Cause	Location
UDP buffering	Network/Kernel
Graylog process backlog	Graylog
Elasticsearch slow indexing	Elasticsearch
CPU/RAM exhaustion	Graylog server
Disk I/O bottleneck	Storage
16. Final Diagnosis Strategy

If delay occurs:

Confirm packet arrival using tcpdump

Check Graylog journal size

Check Elasticsearch health

Monitor CPU & RAM

Verify sort order in Graylog UI

17. Best Practices (Enterprise / CIS)

Use TCP instead of UDP

Enable TLS encryption

Configure disk-assisted queue

Monitor Graylog buffers

Monitor Elasticsearch cluster health

Use log rotation

Secure /var/log permissions

Restrict firewall properly

18. Conclusion

If:

Local logs are instant

Remote packets arrive instantly

But Graylog shows delayed messages

Then the issue is almost certainly:

Graylog processing backlog or Elasticsearch indexing delay

Not rsyslog.

Maintainer Notes

Environment:

CentOS 7

rsyslog default installation

Graylog UDP input on port 8524

Last Updated: 2026