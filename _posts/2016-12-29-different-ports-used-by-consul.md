---
layout: post
title: Different Ports Used by Consul
---

Consul requires up to 5 different ports to work properly, some on TCP, UDP, or both protocols. Below the requirements for each port.
    
* Server RPC (Default 8300). This is used by servers to handle incoming requests from other agents. TCP only.
    
* Serf LAN (Default 8301). This is used to handle gossip in the LAN. Required by all agents. TCP and UDP.
    
* Serf WAN (Default 8302). This is used by servers to gossip over the WAN to other servers. TCP and UDP.
    
* CLI RPC (Default 8400). This is used by all agents to handle RPC from the CLI. TCP only.
    
* HTTP API (Default 8500). This is used by clients to talk to the HTTP API. TCP only.
    * DNS Interface (Default 8600). Used to resolve DNS queries. TCP and UDP.

You can configure consul services to run on different ports by editing the config file. For example setting the DNS interface on port 53 and the HTTP API on port 80.

```ruby
{ 
"ports": { 
            "dns": 53,
            "http": 80
         } 
}
```