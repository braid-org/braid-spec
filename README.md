# Braid: Adding Synchronization to HTTP

This is the working area for the [Braid](https://braid.org) extensions to
HTTP in the [IETF HTTP Working Group](https://httpwg.org/).  These extensions
add Synchronization to HTTP.  They are authored in three documents:

### Braid HTTP — [`draft-toomim-httpbis-braid-http-03.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-braid-http-03.txt)

Braid adds to HTTP:
1. *Versioning* to resources
2. *Subscriptions* to GET requests
3. *Patches* built on Range Requests
4. *Merge-Types* that specify OT or CRDT behavior


### Range Patch — [`draft-toomim-httpbis-range-patch-01.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-range-patch-01.txt)

A uniform approach for expressing changes to state over HTTP.  Generalizes
Range Requests to other HTTP methods.  Defines the replacement of a range with
a new value.

### Merge Types — [`draft-toomim-httpbis-merge-types-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-merge-types-00.txt)

Merge Types specify how to consistently merge a set of simultaneous
conflicting edits to a resource.  If multiple computers implement the same
Merge Type, they can guarantee eventual consistency after arbitrary
multi-writer edits.

### Linked JSON — [`draft-toomim-httpbis-linked-json-00.txt`](https://raw.githubusercontent.com/braid-org/braid-spec/master/draft-toomim-httpbis-linked-json-00.txt)

Linked JSON is an extension of JSON that adds a Link datatype, so that URIs
can be distinguished from ordinary strings.  This allows JSON documents to
be nested inside other JSON documents.


## Contributing

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
