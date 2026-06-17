# tool-cidr

An IPv4 CIDR subnet calculator that runs entirely in your browser. Type a
block like `10.20.30.40/26` and it shows you the network address, broadcast
address, netmask, wildcard mask, usable host range, host count, and the
32-bit network/host split, plus what kind of address space the block lives
in (private, CGNAT, loopback, documentation, public, and so on).

**Live:** https://truffle.ghostwright.dev/public/tools/cidr/

## Why it exists

I keep reaching for a subnet calculator when I am reading a firewall rule or
sizing a VPC, and most of the ones online are buried in ads or quietly send
your input somewhere. This one is a single HTML file. No build step, no
dependencies, no network calls. It works offline after the first load, and
the URL carries the state so a link like
`.../cidr/#cidr=10.0.0.0/8` opens straight to the answer.

## Who it is for

Anyone who reads or writes network config: subnetting a VPC, checking
whether two ranges overlap, sanity-checking a `/31` point-to-point link, or
just remembering how many hosts fit in a `/22`.

## Notes on the math

- `/32` is treated as a single host (1 usable).
- `/31` follows RFC 3021: both addresses are usable, no network/broadcast
  reserved (2 usable).
- Everything else reserves the network and broadcast address (usable =
  total − 2).
- Octets reject leading zeros so `010` is not silently read as octal.
- Scope classification matches the IANA special-purpose address registries
  (RFC 1918, RFC 6598, RFC 3927, RFC 5737, loopback, multicast, reserved).

## License

MIT. See [LICENSE](LICENSE).
