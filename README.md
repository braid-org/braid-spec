# Braid: Adding Synchronization to HTTP

This is the working area for the [Braid](https://braid.news) extensions to
HTTP in the [IETF HTTP Working Group](https://httpwg.org/).  These extensions
add Synchronization to HTTP.  They are authored in three documents:

### Braid HTTP — [`draft-toomim-httpbis-braid-http-00.txt`](https://raw.githubusercontent.com/braid-work/braid-spec/master/draft-toomim-httpbis-braid-http-00.txt)

Braid adds to HTTP:
1. *Versioning* to resources
2. *Subscriptions* to GET requests
3. *Ranges* to PUT and PATCH requests
4. *Merge-Types* that specify OT or CRDT behavior


### Range Patch — [`draft-toomim-httpbis-range-patch-00.txt`](https://raw.githubusercontent.com/braid-work/braid-spec/master/draft-toomim-httpbis-range-patch-00.txt)

A uniform approach for expressing changes to state over HTTP.

### Merge Types — [`draft-toomim-httpbis-merge-types-00.txt`](https://raw.githubusercontent.com/braid-work/braid-spec/master/draft-toomim-httpbis-merge-types-00.txt)

This document defines Merge Types, the structure of the Merge Type system, and
IANA registration procedures for Merge Types.

### NelSON — [`draft-toomim-httpbis-nelson-00.txt`](https://raw.githubusercontent.com/braid-work/braid-spec/master/draft-toomim-httpbis-nelson-00.txt)

NelSON is an extension of JSON that "Ted Nelson would approve of."  Any region
can be framed with a URI and HTTP Metadata.  Allows JSON objects to compose
across websites.  Supports transclusion.

## Contributing

We normally have weekly video meetings on Mondays, but the last week of October
/ first week of November is special because the IETF draft deadline is Nov.
4th. To that end, we are holding daily meetings **Mon-Fri this week, 4:00pm–
5:00pm Pacific** (Oct 28 - Nov 1, 2019).  See https://braid.news.

You are welcome to edit these documents.  To get Github access, send your
login to [Michael](mailto:toomim@gmail.com).  Discuss edits on the
[Braid mailing list](https://groups.google.com/forum/#!forum/braid-http).
After editing, add your name to the authors list at the top and bottom of the
document.

Discussion of the spec should occur on the
[IETF HTTPWG mailing list](https://lists.w3.org/Archives/Public/ietf-http-wg/)
mailing list.  Anyone can contribute; you don't have to join the HTTP Working
Group, because there is no "membership" — anyone who participates in the work
is part of the HTTP Working Group.  See also
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
