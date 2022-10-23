# Step 10. Fail a playback step if the request is not as previously recorded

That is any of **URL**, **method**, **request header**, or **request body**. If they are different in playback than they were in the prior recordings then servertium's playback needs to deliberately fail. If the recorder has a mechanism to alpha-sort or redact headers/bodies, then the playback side also needed that. Pretty-print too. Otherwise and "is different" determination will do false positives.

Servirtium should make the **reason** for the failure available to the test runner. The only reasonable way to do that is inform the test-runner technology of the reason when/if the test runner asks.  So, the same way there is a `setContext(string)` method/function from the point of view of the test runner, there should also be a `getLastError()` mechanism to pull the failure details back to the test runner and inform the developer. That could be via an "after" test mechanism (after each, not after all/suite).  See below:

New tests for the implementation repo not the demo/tck one:

## Request Header

This recording https://raw.githubusercontent.com/servirtium/README/master/broken_recordings/request_headers_that_never_happened 
claims to be a recording of a site but it is not as you can plainly see.  Your test should fail because there were unexpected headers in the request.

In the attempt to use this recording for playback purposes your **direct HTTP-get** (in the middle of your test) should **not** specify `should_fail_here` in the request headers.  Servirtium should note the differet request headers and reply without response (say close of socket), and store the the reason for the failure for a `servirtium.getLastError()` call from the test tearDown/afterTest expectation check.  And that last should confirm that the right thing happened.  Most likely this is a wholly separate test class/spec in your test-base. The error should say 'should_fail_here request header encountered but not expected' (or similar). 

Duplicate that test but make a difference to this one 'should_fail_here' was in your request headers going to servirtium on port 61417, but the value was difference. The test should still fail but the tearDown/afterTest quivlent should report on the difference of the value to the otherwise expcted header.

## Request Body

This recording https://raw.githubusercontent.com/servirtium/README/master/broken_recordings/request_body_that_never_happened 
claims to be a recording of a site but it is not as you can plainly see.  Your test should fail because there were unexpected body in the request.

In the attempt to use this recording for playback purposes your **direct HTTP-get** (in the middle of your test) should not specify anything for the request body (normal for GET).  Servirtium should note the different request body and reply without response (say close of socket) and store the the reason for the failure for a `servirtium.getLastError()` call from the test tearDown/afterTest expectation check.  And that last should confirm that the right thing happened.  Most likely this is a wholly separate test class/spec in your test-base. The error should say 'request body different to expectation' (or similar) and have details as to the difference.
