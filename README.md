pcap-reassembler
================

Reassembles UDP/TCP packets into application layer messages. May also
extract data from different OSI layers.

Introduction
------------

pcap-reassembler is a tool which helps analyzing application layer protocol
data without having to inspect segmented transport level payloads.
For TCP, application layer messages are reassembled through analysis of
acknowledgement numbers between segments. For UDP, each datagram payload is
interpreted as an application layer message.

As of now, pcap-reassembler is compatible with Ethernet as link layer protocol,
IPv4 as network layer protocol, and TCP or UDP as transport layer protocols. The
transport layer protocol is automatically detected from the IP header protocol
flag.

pcap-reassembler is implemented through [pylibpcap](http://pylibpcap.sourceforge.net/).

Installation
------------

Install pcap-reassembler with ```python setup.py install```

Usage
-----

```python
>>> from pcap_reassembler import PcapReassembler, address_to_string
>>> reassembler = PcapReassembler()
>>> messages = reassembler.load_pcap('http.cap')
>>> msg = messages[0]
>>> msg.payload
'GET /download.html HTTP/1.1\r\nHost: www.ethereal.com\r\nUser-Agent: Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.6) Gecko/20040113\r\nAccept: text/xml,application/xml,application/xhtml+xml,text/html;q=0.9,text/plain;q=0.8,image/png,image/jpeg,image/gif;q=0.2,*/*;q=0.1\r\nAccept-Language: en-us,en;q=0.5\r\nAccept-Encoding: gzip,deflate\r\nAccept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7\r\nKeep-Alive: 300\r\nConnection: keep-alive\r\nReferer: http://www.ethereal.com/development.html\r\n\r\n'
>>> address_to_string(msg.src_addr)
'145.254.160.237'
```

Limitations
-----------

pcap-reassembler does not yet support IP fragmentation or IPv6. Also the only
transport layer protocols that are supported are TCP and UDP.

License
-------

Distributed under the MIT license. See the ```LICENSE``` file.
