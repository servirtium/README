# Step 8. Redaction, Mask, Delete, and Mutate operations

Sometimes things have to be changed in request headers and/or request body that is saved as markdown in a recording
Similarly things may have to be changed in response headers and/or response body.  

Related things that were recorded in a certain way, may have to be changed again in playback. You might have morphed 
`Date: Wed, 21 Oct 2019 07:28:00 GMT` to `Date: todays's-date-paul-was-here` for the purposes of the recording, but
in playback it needs to be changed again from `Date: todays's-date-paul-was-here` to `Date: Sun, 9 Feb 2020 11:18:03 GMT` 
so that tests still pass.

Then there's also removal of headers (and parts of a body) at both request and response level, that's needed.

For any of these it may be a good idea to get regex and non regex ways working.

You'll note that the recording generates many differences between recordings (back to back). That is a good list of things to check off for mutation, mask, redaction, deletion.

You'll also note that some of the same Redaction, Mask, Delete, and Mutate operations should be in playback. Or perhaps: un_redact, un_mask, un_mutate.
