# Simple GTP Gateway example

This example make use of libgtpnl from osmocom to create a GTP tunnel
and send some traffic.

## Setup

First, get the example:

```console
git clone https://github.com/abousselmi/gtp-example.git
cd gtp-example
```

Second, you need to clone libgtpnl and compile it:

```console
git clone https://git.osmocom.org/libgtpnl
cd libgtpnl
autoreconf -fi
./configure
make
sudo make install
sudo ldconfig
```

Now we need to copy the example script where we have the gtp wrappers:

```console
cp ../example.sh ./tools
cd tools
```

Now you can run the example and enjoy:

```console
./example.sh start
```

To destroy everything, you can do:

```console
./example.sh stop
```

## Sample output

```console
./example.sh start
[INFO] create veth pairs
[INFO] create network namespaces
[INFO] attribute each veth pair to its correspondent netns
[INFO] set ip addresses of veth pairs and loopbacks
[INFO] enable veth and lo interfaces
[INFO] create gtp devices (run in bg mode)
[INFO] configure mtu of gtp devices
WARNING: attaching dummy socket descriptors. Keep this process running for testing purposes.
WARNING: attaching dummy socket descriptors. Keep this process running for testing purposes.
[INFO] create gtp tunnels
[INFO] version 1 tei 200/100 ms_addr 192.168.0.200 sgsn_addr 172.100.0.200
[INFO] version 1 tei 100/200 ms_addr 192.168.0.100 sgsn_addr 172.100.0.100
[INFO] configure routes using gtp devices

You can go for e.g.:
  ip netns exec ns-gtp-100 ping 192.168.0.200
  ip netns exec ns-gtp-200 ping 192.168.0.100

Using tshark you will see ICMP pckets encapsulated in GTP
```

## Credits

Reference: [Kentaro Ebisawa](https://www.slideshare.net/kentaroebisawa/using-gtp-on-linux-with-libgtpnl)

## License

MIT
