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

### Subscriptions: [`draft-toomim-httpbis-braid-subscriptions-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-subscriptions-00.txt)

Subscriptions turn a GET into a stream of changes.  The client adds the
Subscribe header, and the server responds with the current state, and then
with each change as it happens.  Each change is an ordinary HTTP response, so
every cache along the way can store and serve it.

Two drafts extend Subscriptions:

### Subscriptions Caching: [`draft-toomim-httpbis-braid-subscriptions-caching-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-subscriptions-caching-00.txt)

When a cache subscribes, its subscription becomes a validation that keeps
going.  The origin sends the cache each change as it happens, so while the
subscription stays connected, the cache knows its copy is current.  It serves
every reader at its edge from that subscription, without asking the origin
again.

### Poll and Push: [`draft-toomim-httpbis-braid-poll-and-push-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-poll-and-push-00.txt)

Poll and Push brings subscriptions to servers, and paths, that can't hold a
response open.  A client can long-poll, with a GET that the server holds until
the next change, or an origin can push each change to a subscription gateway,
which serves its subscribers for it.  Each message names the version it builds
on, so no message depends on a connection staying open.

### Updates: [`draft-toomim-httpbis-braid-updates-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-updates-00.txt)

Updates make each change mean the same thing in both directions.  A client
sends a patch to a server in a PUT, and the server sends the same patch on to
other clients, in a response.  Every peer that replays the same updates reaches
the same state, whether it's a client, a server, or a cache in between.

### Versions: [`draft-toomim-httpbis-braid-versions-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-versions-00.txt)

Versions give HTTP a sense of time.  A message can name the point in history
that it's at, and the points just before it, so a client can GET the state at
any version, and say which version its PUT builds on.  History can branch and
merge, as a DAG, and every peer names each point the same way.

### Merge Types: [`draft-toomim-httpbis-braid-merge-types-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-merge-types-00.txt)

With Merge Types, many peers can edit one resource at once, and still agree.  A
Merge Type names the algorithm, OT or CRDT, that every peer uses to merge
parallel edits, so they all reach the same state.  It builds on Versions, to
tell which edits were parallel, and on Updates, to know what each one changed.

### Multiresponse: [`draft-toomim-httpbis-braid-multiresponse-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-multiresponse-00.txt)

Multiresponse fits many responses into one.  A 209 Multiresponse holds a
sequence of ordinary responses, such as a span of a resource's history, or a
subscription's changes as they happen.  Each one still responds to a request of
its own, so caches can store them one by one.

## The syntax they share

### Simpler Fields: [`draft-toomim-httpbis-simpler-fields-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-simpler-fields-00.txt)

Simpler Fields keeps every new header field one regular expression away.  It's
a profile of Structured Fields, with special characters in strings
percent-encoded, so a light client can parse a field with a regular expression,
and a full Structured Fields parser reads it unchanged.  Every new header field
in these drafts uses it.

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
