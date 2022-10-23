## Confirm the Playback node barfs clearly for unexpected request details

This is for the implementation repo not the demo/tck one

### Request Header

This recording https://raw.githubusercontent.com/servirtium/README/master/broken_recordings/request_body_that_never_happened 
claims to be a recording of a site but it is not as you can plainly see.  Your test should fail because there were unexpected headers in the request.

In the attempt to use this recording for playback purposes your **direct HTTP-get** (in the middle of your test) should not specify `should_fail_here` in the request headers.  Servirtium should note the differet request headers in the recording to the request through port 61417 and reply without response, and store the the reason for the failure for a `servirtium.getLastError()` call from the test tearDown/afterTest expectation check.  And that last should confirm that the right thing happened.  Most likely this is a wholly separate test class/spec.

### Request Body
