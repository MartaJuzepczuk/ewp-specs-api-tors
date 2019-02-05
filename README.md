Unbounded Transcripts of Records API
====================================

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


Summary
-------

This document describes the **Unbounded Transcripts of Records API**.
This API is implemented by the receiving institution. It allows the sending
institution to retrieve Transcripts of Records issued by the receiving
institution.

The transcript in this API is identified by its own identifier
(in opposite to the [Incoming Mobility ToRs API][imobilitiy-tors-api],
where it is identified by the mobility id). This allows to send transcripts
without former exchange of mobilities via [Outgoing Mobilities API][omobilities-api].

Note that all the transcripts that we write about here are actually related to student mobilities.
They are only being sent without the context of the mobility.


Security and permissions
------------------------

This version of this API uses [standard EWP Authentication and Security, Version 2][sec-v2].
Server implementers choose which security methods they support by declaring them
in their Manifest API entry.

This API handles data which is considered private. Server implementers are
allowed to forbid less-secure methods of authentication and encryption for this
API (by dropping support for them). Currently, we leave it for the server
implementers to decide which methods are "secure enough". These recommendations
MAY change in the future.

Only selected Transcripts of Records should be accessible to the caller:

 * If a ToR has not been approved as "ready for recognition" yet, then it
   SHOULD NOT be accessible via this API (see discussion
   [here](https://github.com/erasmus-without-paper/ewp-specs-mobility-flowcharts/issues/3#issuecomment-327196926)).

 * If the caller covers the sending HEI of the given mobility, then he MUST be
   allowed read access to the mobility's corresponding ToR.

 * If the caller covers the receiving HEI (yourself) of the given mobility,
   then he MAY be allowed read access to the mobility's corresponding ToR. (It
   seems reasonable to do so, but we leave this decision to your team.)

 * All other callers SHOULD NOT be allowed to view the ToR.

 * Note, that servers will need to verify these access rights for each ID on
   the `tor_id` list. It is possible that the caller has access to only
   some of the mobilities. (If this seems problematic, then you can always
   simply set your `<max-tor-ids>` to `1`.)


Endpoints to be implemented
---------------------------

Server implementers MUST:

 * Implement the [`get` endpoint](endpoints/get.md).
 * Implement the [`index` endpoint](endpoints/index.md).
 * Put the URLs of these endpoints in their [manifest file][discovery-api], as
   described in [manifest-entry.xsd](manifest-entry.xsd).

The details on each of these endpoints are described on separate pages of this
API specification (use the links above).


[develhub]: http://developers.erasmuswithoutpaper.eu/
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management#statuses
[discovery-api]: https://github.com/erasmus-without-paper/ewp-specs-api-discovery
[imobilitiy-tors-api]: https://github.com/erasmus-without-paper/ewp-specs-api-imobility-tors
[omobilities-api]: https://github.com/erasmus-without-paper/ewp-specs-api-omobilities
[sec-v2]: https://github.com/erasmus-without-paper/ewp-specs-sec-intro/tree/stable-v2
