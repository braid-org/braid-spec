# Braid-HTTP: State Synchronization for HTTP

This repository holds the Braid-HTTP extensions to HTTP, which we develop in
the open at [braid.org](https://braid.org), and contribute to the
[IETF HTTP Working Group](https://httpwg.org/).  Each extension addresses one
limitation of HTTP, and works alone, or together with the others.

## Overview

### Braid-HTTP: [`draft-toomim-httpbis-braid-http-05.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-http-05.txt)

Braid-HTTP extends HTTP from transferring state to synchronizing it.  With it,
a website can synchronize with any other website's state by its URL alone,
just as a page can link to any other page.  The HyperText Transfer Protocol
becomes a HyperState Synchronization Protocol.  Start here.

## The extensions

### Versions: [`draft-toomim-httpbis-braid-versions-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-versions-00.txt)

HTTP can't name a point in a resource's history.  Versions names points in
time, with the events of a DAG, so that a client can GET the state at a
version, and say which version its PUT builds on.

### Updates: [`draft-toomim-httpbis-braid-updates-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-updates-00.txt)

HTTP can't express a change the same way from client to server and from
server to client.  Updates defines snapshots, patches, and deletions that mean
the same thing in a request and in a response, so every peer that replays
them reaches the same state.

### Multiresponse: [`draft-toomim-httpbis-braid-multiresponse-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-multiresponse-00.txt)

Each HTTP request gets one response.  Multiresponse defines the 209
Multiresponse status code, whose content holds several responses, and
application/http-history, a format for a resource's responses over time.

### Subscriptions: [`draft-toomim-httpbis-braid-subscriptions-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-subscriptions-00.txt)

A server responds to a GET once, so the client doesn't hear when the resource
changes later.  With a subscription, the server sends the current state, and
then each change as it happens.  Each response is the one that the server
would have sent to the same GET just after the change, so a cache can store
it, and can answer requests from its copy for as long as the subscription
lasts.

Two drafts extend Subscriptions:

### Subscriptions Caching: [`draft-toomim-httpbis-braid-subscriptions-caching-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-subscriptions-caching-00.txt)

A cache can subscribe to a resource, as any client can.  It stores each
response in the subscription, answers requests from its copy while the
subscription is continuously validating, and serves many subscribers of its
own from one subscription to the origin server.

### Poll and Push: [`draft-toomim-httpbis-braid-poll-and-push-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-poll-and-push-00.txt)

Some origin servers can't hold a response open, and on some paths a proxy
buffers each response until it ends.  For them, Poll and Push defines two
more subscription modes: long polling, in which the client sends a GET for
each change, and webhooks, in which the origin server pushes each change to a
subscription gateway.

### Merge Types: [`draft-toomim-httpbis-braid-merge-types-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-merge-types-00.txt)

HTTP doesn't say how to merge changes that peers make in parallel.  A Merge
Type says how to merge them, so that every peer reaches the same state.  It
builds on Versions and Updates.

## The syntax they share

### Simpler Fields: [`draft-toomim-httpbis-simpler-fields-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-simpler-fields-00.txt)

Simpler Fields is a profile of Structured Fields that a light client can
parse with a regular expression.  The new header fields of all these drafts
use it.

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

Updates replaces Range Patch,
[`draft-toomim-httpbis-range-patch-01.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-range-patch-01.txt).
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
