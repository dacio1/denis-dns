Denis is a simple DNS server implemented in java. It only supports query type "A". It is designed to be simple, easy to read and easy to extend.

Denis has very simple caching, it forwards the request to another DNS server if it can't find a requested domain name in the cache. Denis resolves host information not only from other DNS servers, it could also fetch host information from some web sites such as www.ip.cn. So theoretically, Denis could resolve hosts correctly even if the hosts are blocked by other dns servers.

## Features ##
  * Recursive resolving
  * Simple caching
  * Handling query type "A"
  * Interactive shell
  * Could show cache in the format which is acceptable in /etc/hosts
  * **Resolving through web**, providing the ability to bypass DNS blockers.

## Problems ##
  * It handles all requests in **one** thread, it might be slow for heavy load
  * It's slow, I don't know why
  * Caching is implemented with a simple array list. You could use other data structures
  * It does not have any default config files, you need to load config files manually
  * Currently **resolving through web** only supports www.ip.cn. You need to write your own parser if you need to support other servers.

## How to play ##
  1. Compile the java code. I assume you know how to compile if you know java
  1. Run command `java com.appspot.trent.denis.Denis`. Then you will have the program running. Here's the screen captured from my computer:

```
# java com.appspot.trent.denis.Denis
>> load /root/denis.prop
>> help
help -- show help message
resolve domainName -- resolve host
cache -- show cache items
save fileName -- save cache to fileName
load filename -- load cache from fileName
exit -- exit shell
>>  
```

You might need to change the source file DnsServer to specify your upper dns server.

If you want to get IP information from other web resolvers, you can take the file HttpResolver as an example.

Here's a little trick: you could run command "`cache`" in the interactive shell, and paste the result to the file /etc/hosts (I'm a Linux user), this would accelerate resolving greatly.

**NOTE: This project needs great work to do before it is fully available. You can play with it, but please do not expect too much from it.**

## References ##
The only reference is the book _TCP/IP illustrated Volume 1_ by **Richard Steves**. I was too lazy to read RFC docs (RFC1034 and RFC1035).