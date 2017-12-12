```sh
$> editcap -h
```

```
Editcap (Wireshark) 2.4.1 (v2.4.1-0-gf42a0d2)
Edit and/or translate the format of capture files.
See https://www.wireshark.org for more information.

Usage: editcap [options] ... <infile> <outfile> [ <packet#>[-<packet#>] ... ]

<infile> and <outfile> must both be present.
A single packet or a range of packets can be selected.

Packet selection:
  -r                     keep the selected packets; default is to delete them.
  -A <start time>        only output packets whose timestamp is after (or equal
                         to) the given time (format as YYYY-MM-DD hh:mm:ss).
  -B <stop time>         only output packets whose timestamp is before the
                         given time (format as YYYY-MM-DD hh:mm:ss).

Duplicate packet removal:
  --novlan               remove vlan info from packets before checking for duplicates.
  -d                     remove packet if duplicate (window == 5).
  -D <dup window>        remove packet if duplicate; configurable <dup window>.
                         Valid <dup window> values are 0 to 1000000.
                         NOTE: A <dup window> of 0 with -v (verbose option) is
                         useful to print MD5 hashes.
  -w <dup time window>   remove packet if duplicate packet is found EQUAL TO OR
                         LESS THAN <dup time window> prior to current packet.
                         A <dup time window> is specified in relative seconds
                         (e.g. 0.000001).
  -a <framenum>:<comment> Add or replace comment for given frame number

  -I <bytes to ignore>   ignore the specified number of bytes at the beginning
                         of the frame during MD5 hash calculation, unless the
                         frame is too short, then the full frame is used.
                         Useful to remove duplicated packets taken on
                         several routers (different mac addresses for
                         example).
                         e.g. -I 26 in case of Ether/IP will ignore
                         ether(14) and IP header(20 - 4(src ip) - 4(dst ip)).

           NOTE: The use of the 'Duplicate packet removal' options with
           other editcap options except -v may not always work as expected.
           Specifically the -r, -t or -S options will very likely NOT have the
           desired effect if combined with the -d, -D or -w.

Packet manipulation:
  -s <snaplen>           truncate each packet to max. <snaplen> bytes of data.
  -C [offset:]<choplen>  chop each packet by <choplen> bytes. Positive values
                         chop at the packet beginning, negative values at the
                         packet end. If an optional offset precedes the length,
                         then the bytes chopped will be offset from that value.
                         Positive offsets are from the packet beginning,
                         negative offsets are from the packet end. You can use
                         this option more than once, allowing up to 2 chopping
                         regions within a packet provided that at least 1
                         choplen is positive and at least 1 is negative.
  -L                     adjust the frame (i.e. reported) length when chopping
                         and/or snapping.
  -t <time adjustment>   adjust the timestamp of each packet.
                         <time adjustment> is in relative seconds (e.g. -0.5).
  -S <strict adjustment> adjust timestamp of packets if necessary to ensure
                         strict chronological increasing order. The <strict
                         adjustment> is specified in relative seconds with
                         values of 0 or 0.000001 being the most reasonable.
                         A negative adjustment value will modify timestamps so
                         that each packet's delta time is the absolute value
                         of the adjustment specified. A value of -0 will set
                         all packets to the timestamp of the first packet.
  -E <error probability> set the probability (between 0.0 and 1.0 incl.) that
                         a particular packet byte will be randomly changed.
  -o <change offset>     When used in conjunction with -E, skip some bytes from the
                         beginning of the packet. This allows one to preserve some
                         bytes, in order to have some headers untouched.

Output File(s):
  -c <packets per file>  split the packet output to different files based on
                         uniform packet counts with a maximum of
                         <packets per file> each.
  -i <seconds per file>  split the packet output to different files based on
                         uniform time intervals with a maximum of
                         <seconds per file> each.
  -F <capture type>      set the output file type; default is pcapng. An empty
                         "-F" option will list the file types.
  -T <encap type>        set the output file encapsulation type; default is the
                         same as the input file. An empty "-T" option will
                         list the encapsulation types.

Miscellaneous:
  -h                     display this help and exit.
  -v                     verbose output.
                         If -v is used with any of the 'Duplicate Packet
                         Removal' options (-d, -D or -w) then Packet lengths
                         and MD5 hashes are printed to standard-error.

```