# CoreDNS-Docker

<!--- mdtoc: toc begin -->

1. [Synopsis](#synopsis)
2. [Prerequisites](#prerequisites)
3. [How to run?](#how-to-run-)<!--- mdtoc: toc end -->

## Synopsis

This is a simple [CoreDNS](https://coredns.io) docker setup that is intended to be running as a system wide DNS Server and therefore by default exposing port 53. It can and has to be installed without any other DNS service blocking port 53.

The `conf/Corefile` holds a very basic example configuration demonstrating how to get custom answers to `A` queries. Note that ipv6 addresses (`AAAA`) or any other type of records aren't configured in the example. Needing any of these would require introducing zones and change the configuration layout a little. But for now we focus on simplicity which probably is perfectly fine for the present use case. The example setup reponds with configured ips for `example.aip` and `example.escience`.

The Container mounts its configuration as a volume to make later editing easier. It has auto reload enabled and applies modified configurations without restart. The config that is actually used by a running container is located in `vol/conf`. If the folder does not contain a `Corefile` the one from `conf` will be copied during the build process.

## Prerequisites

1. Having [Task](taskfile.dev/) because it is used to simplify build and run processes

2. As stated above port 53 needs to be free which obviously requires the system's default DNS Resolver to be disabled

3. The `/etc/resolv.conf` has to point to our server. It should look like the following.

   ```
   nameserver 127.0.0.1
   ```

4. Before the docker build this setup tries to fetch the CoreDNS binary from the system. Its path needs to be in `$PATH` so that the command `which coredns` delivers something processable.

## How to run?

As usual a `Taskfile` can be found.

```shell
# build and run
task

# run, but expose a different port which is provided as argument
task -- 5353
task rebuild -- 6464

# list of all available tasks
task -l
```
