# Raw Traffic
This is a simple program to capture IPv4 network traffic and save it to a binary file via the [libpcap](https://www.tcpdump.org/) network traffic capture library.

## Dependencies
This program requires the [libpcap](https://www.tcpdump.org/) development libraries. 

If you're on Debian, you can install these libraries with the following command: 
```
sudo apt-get install libpcap-dev
```

## Compiling
If you're compiling with `gcc`, you must include `-l pcap` to search the `libpcap` library when linking.
```
gcc rawtraffic.c -o rawtraffic -lpcap
```

## Usage
```
./rawtraffic <interface> <port> [<savefile name>]
```

The interface and port number arguments are mandatory. You can optionally specify the name of the file to save the captured packets to. If you do not specify a filename as the third argument, then the default filename `capture` will be used.

By default, this program will capture 2 packets before stopping. You can set the desired number of packets to be captured by changing the value of this variable:
```
#define PCOUNT 2
```

Upon setting `PCOUNT` to 0, the capture will continue indefinitely until an ending condition occurs. See `pcap_loop(3PCAP)` for details.

### Example
Listen to port `8000` on the loopback interface:
```
./rawtraffic lo 8000
```

Listen to port `25` on the enp4s0 interface, and save captured packets to the file `emails`.
```
./rawtraffic enp4s0 25 emails
```

Capture packets indefinitely:
```
#define PCOUNT 0
```