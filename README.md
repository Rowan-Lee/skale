# skale
Tired of getting ratelimited? Skale aims to allow you to scale your requests across proxied connections.

# Specification / Design Plan:
## Basic Intended Function:
### Setup:
- Read configuration
- Get proxies
### Loop:  
- Await request
- Forward request to proxy, dispatch thread to:
  - Await return
  - Return value(s)

## Intended Features:
- Configuration:
  - Proxy:
    - Source (where to fetch or read lists)
    - Type (e.g. SOCKS5 or HTTP)
  - Connections:
    - Keep open or open on demand
    - Amount of requests per proxy connection (i.e. self-imposed ratelimit, 0ms being the default, aka off)
    - Amount allowed at a time
  - Misc:
    - Automatic ratelimit detection (sacrifice a proxy to determine maximum request rate before IP-banned/ratelimited from a given resource) (on/off)
    - Auto-Conf: use AI magic or something to determine the optimal configuration, as opposed to the user manually configuring.
- Load balancing
- Intelligently caching data

## Required pre-written features:
- Async: Tokio
- Data serialization/deserialization: Serde
- HTTP: Rocket
- File IO: STD
- Extra networking?: STD