# Caching in NoFlo <br/>[![Build Status](https://secure.travis-ci.org/kenhkan/noflo-cache.png?branch=master)](http://travis-ci.org/kenhkan/noflo-cache) [![Dependency Status](https://david-dm.org/kenhkan/noflo-cache.png)](https://david-dm.org/kenhkan/noflo-cache) [![NPM version](https://badge.fury.io/js/noflo-cache.png)](http://badge.fury.io/js/noflo-cache) [![Stories in Ready](https://badge.waffle.io/kenhkan/noflo-cache.png)](http://waffle.io/kenhkan/noflo-cache)

Provide caching so packets are presisted in memory for future connections. This is almost always a necessary tool when you have asynchronous operation!


## Installation

`npm install --save noflo-cache`

## Usage

* [cache/Cache](#Cache)
* [cache/CacheByGroup](#CacheByGroup)

Listed in-ports in bold are required and out-ports in bold always produce IPs.


### Cache

Save incoming IPs and send the saved IPs to port 'out' upon any data IP from
'ready'

#### In-Ports

* *IN*: The value to cache
* *READY*: Release a particular cache by key. Release all cache if no key is
  provided
* KEY: The key associated with the value
* SIZE: The maximum size
* KEEP: Whether to keep the cached value or not after release

#### Out-Ports

* *OUT*: The cached value


### CacheByGroup

Like `cache/Cache`, but the to-be-cached incoming value is automatically
associated with the key that is the group (and the only group) to the incoming
value. For instance, 'abc' would be the key in the following case:

    CONNECT:
    BEGINGROUP: 'abc'
    DATA: 'things to cache'
    ENDGROUP: 'abc'
    DISCONNECT:

#### In-Ports

* *IN*: The value to cache. The group is used as the caching key.
* *READY*: Release the cached value. The group of the incoming is used as the
  the caching key.
* SIZE: The maximum size
* KEEP: Whether to keep the cached value or not after release

#### Out-Ports

* *OUT*: The cached value
