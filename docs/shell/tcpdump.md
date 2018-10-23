# tcpdump

## Introduction

Reference: man tcpdump

tcpdump - dump traffic on a network

SYNOPSIS:

> tcpdump [options] \[expression]

OPTIONS:

> -i Listen on interface
>
> -w Write the raw packets to file rather than parsing and printing them out.
>
> -r Read packets from file.
>
> -s Snarf snaplen bytes of data from each packet rather than the default of 65535 bytes. Setting snaplen to 0 sets it to the default of 65535.
>
> -S Print absolute, rather than relative, TCP sequence numbers.
>
> -nn Don't convert host addresses to names.  This can be used to avoid DNS lookups.

EXPRESSION:

> man pcap-filter

##EXPRESSION

The filter expression consists of one or more *primitives*.  *Primitives* usually consist of an id (name or number) preceded by one or more *qualifiers*.  There are three different kinds of *qualifier*:

### type

Possible types are host, net , port and portrange.

### dir

Possible directions are src, dst, src or dst, src and dst, ra, ta, addr1, addr2, addr3, and addr4.

### proto

Possible protos are: ether, fddi, tr, wlan, ip, ip6, arp, rarp, decnet, tcp and udp.

```reStructuredText
'udp port 53'
'dst 202.54.1.5 (port 21 or 20'
```

