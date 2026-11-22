# Braid-HTTP: State Synchronization for HTTP

This repository holds the Braid-HTTP extensions to HTTP, which we develop in
the open at [braid.org](https://braid.org), and contribute to the
[IETF HTTP Working Group](https://httpwg.org/).  Each extension addresses one
limitation of HTTP, and works alone, or together with the others.

## Braid-HTTP Specs

Braid-HTTP extends HTTP from transferring state to synchronizing it.  With it,
a website can synchronize with any other website's state by its URL alone,
just as a page can link to any other page.  The HyperText Transfer Protocol
becomes a HyperState Synchronization Protocol.

- [`draft-braid-http`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-http-06.txt)
  explains how the individual Braid-HTTP pieces (below) compose as aspects of a synchronization protocol

### Subscriptions

*Subscriptions* extends HTTP with a `Subscribe:` header, that tells a server to
first respond with the current state, and then promise to send all future
updates until the subscription ends.  Each update is itself an HTTP response
(see the `updates` draft below), which can be cached and served by
intermediaries.

- [`draft-braid-subscriptions`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-subscriptions-01.txt)
  defines the `Subscribe:` header, and specifies its semantics.
  - [`draft-braid-subscriptions-caching`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-subscriptions-caching-01.txt)
    specifies how a cache (like a CDN or proxy) should store the responses in a
    subscription, serve requests from a continuously validated copy, and share
    one upstream subscription among many subscribers
  - [`draft-braid-poll-and-push`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-poll-and-push-01.txt)
    specifies the additional poll and push modes, which support servers that run
    as serverless functions or on shared hosting, and paths through proxies that
    buffer each response until it ends

Subscriptions improve cache performance and functionality:

 - Caches that hold a live subscription to the origin are "continuously validated", and can skip the 1RTT to re-validate a stale cache entry.
 - Origin servers can push updates directly to a cache, instead of waiting for a client to pull them, which reduces cache update times from 1.5RTT to 0.5RTT.
 - Caches (like CDNs) can support live-updating state, and fan it out to multiple clients.  This eliminates the need for WebSockets, which takes WebSocket load off the origin.  A single origin subscription can then serve any number of clients.
 - For origin servers that lack the ability to hold long-lived connections, an intermediary can instead accept updates via webhook or long-polling, which it can then translate into a stream for any number of clients.  This allows legacy web architectures (such as cgi-bin and PHP) to serve realtime state.


### Updates

Updates make each change mean the same thing in both directions.  A client
sends a patch to a server in a PUT, and the server sends the same patch on to
other clients, in a response.  Every peer that replays the same updates reaches
the same state, whether it's a client, a server, or a cache in between.

- [`draft-braid-updates`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-updates-01.txt)
  specifies snapshots, patches, and deletions, the same way in requests and in
  responses

### Versions

Versions give HTTP a sense of time.  A message can name the point in history
that it's at, and the points just before it, so a client can GET the state at
any version, and say which version its PUT builds on.  History can branch and
merge, as a DAG, and every peer names each point the same way.

- [`draft-braid-versions`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-versions-01.txt)
  specifies the Version and Parents headers, and how each HTTP method reads and
  writes state at a version

### Multiresponse

Multiresponse fits many responses into one.  A 209 Multiresponse holds a
sequence of ordinary responses, such as a span of a resource's history, or a
subscription's changes as they happen.  Each one still responds to a request of
its own, so caches can store them one by one.

- [`draft-braid-multiresponse`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-multiresponse-01.txt)
  specifies the 209 Multiresponse status code, and the application/http-history
  media type

### Merge Types

With Merge Types, many peers can edit one resource at once, and still agree.  A
Merge Type names the algorithm, OT or CRDT, that every peer uses to merge
parallel edits, so they all reach the same state.  It builds on Versions, to
tell which edits were parallel, and on Updates, to know what each one changed.

- [`draft-braid-merge-types`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-merge-types-01.txt)
  specifies the Merge-Type header, and a registry of merge types

## HTTP Utility Specs

### Simpler Fields

Simpler Fields makes HTTP headers easier to parse.  It's
a profile of Structured Fields, with special characters in strings
percent-encoded, so a light client can parse a field with a regular expression,
and a full Structured Fields parser reads it unchanged.

- [`draft-simpler-fields`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-simpler-fields-01.txt)
  specifies the profile, and how a client parses a field with a short regular
  expression of its own

## Data Schema Specs

### Linked JSON

Linked JSON is an extension of JSON that adds a Link datatype, so that URIs
can be distinguished from ordinary strings.  This allows JSON documents to
be nested inside other JSON documents.

- [`draft-linked-json`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-linked-json-00.txt)
  specifies the Link datatype, and its optional metadata, which can name a
  version or a slice of the data to link to, or cache a prefetched result

### NelSON

NelSON is similar to Linked JSON, but expressed as "a JSON that Ted Nelson would approve of."  It defines hypermedia transclusions in JSON.

- [`draft-nelson`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-nelson-00.txt)


## Where to start reading

Application developers can start with Subscriptions, which shows how a page
subscribes to a resource with a GET, and then read Updates, to send changes as
patches.

CDN and cache implementers can start with Subscriptions Caching, which shows
how one subscription to the origin serves every subscriber at an edge, and
keeps the cache current for plain GETs.

Origins on serverless or shared hosting, which can't hold a response open, can
start with Poll and Push.

## Earlier drafts

- The [Range-Patch](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-range-patch-01.txt) has now been replaced by the Updates draft above.

Earlier versions of the drafts are in [`old/`](old/).


## Contributing

You are welcome to edit these documents.  To get Github access, send your
login to [Michael](mailto:toomim@gmail.com).  Discuss edits on the
[Braid-HTTP mailing list](https://groups.google.com/forum/#!forum/braid-http).
After editing, add your name to the authors list at the top and bottom of the
document.

Discussion of the spec should occur on the
[IETF HTTPWG mailing list](https://lists.w3.org/Archives/Public/ietf-http-wg/).
Anyone can contribute; you don't have to join the HTTP Working Group, because
there is no "membership": anyone who participates in the work is part of the
HTTP Working Group.  See also
[Contributing to the HTTP Working Group](https://github.com/httpwg/http-extensions/blob/master/CONTRIBUTING.md).

All material in this repository is considered Contributions to the
([IETF](https://www.ietf.org/)) Standards Process, as defined in the
intellectual property policies of IETF currently designated as
[BCP 78](https://www.rfc-editor.org/info/bcp78),
[BCP 79](https://www.rfc-editor.org/info/bcp79) and the
[IETF Trust Legal Provisions (TLP) Relating to IETF Documents](http://trustee.ietf.org/trust-legal-provisions.html).
Any edit, commit, pull request, issue, comment or other change made to this
repository constitutes Contributions to the IETF Standards Process
(https://www.ietf.org/).
You agree to comply with all applicable IETF policies and procedures,
including, BCP 78, 79, the TLP, and the TLP rules regarding code components
(e.g. being subject to a Simplified BSD License) in Contributions.
