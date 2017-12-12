Examine the following two files :
```sh
./tracefiles/cli/clientside-ftp.pcapng
./tracefiles/cli/serverside-ftp.pcapng
```

Extract the timestamp of the of the first packet in each of the files.
```sh
$> tshark -r ./tracefiles/cli/clientside-ftp.pcapng -T fields -e frame.time -c 5
$> tshark -r ./tracefiles/cli/serverside-ftp.pcapng -T fields -e frame.time -c 5
```

Examine the following file (94000 packets):
```sh
./tracefiles/cli/tcp-packetloss.pcapng
```

Split the file with a maximum of 20000 packets
```sh
$> editcap -c 20000 ./tracefiles/cli/tcp-packetloss.pcapng ./tracefiles/cli/split-tcp-packetloss.pcapng
```
