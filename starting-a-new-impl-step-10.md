# Step 10. Fail a playback step if the request is not as previously recorded

That is any of **URL**, **method**, **request header**, or **request body**. If they are different in playback than 
they were in the prior recordings then servertium's playback needs to deliberately fail. If the recorder has a 
mechanism to alpha-sort or redact headers/bodies, then the playback side also needed that. Pretty-print too. 
Otherwise and "is different" determination will do false positives.

Close of socket is an admirable way to communicate failure. 

Serverium should make the **reason** for the failure available to the test runner. The only
reasonable way to do that is inform the test-runner technology of the reason when/if the test runner asks.  So
the the same way there is a `setContext(string)` method/function from the point of view of the test runner,
there should also be a `getLastError()` mechanism to pull the failure details back to the test runner and 
inform the developer. That could be via an "after" test mechanism (after each, not after all/suite).
