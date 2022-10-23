## Confirm the Playback node barfs clearly for unexpected request details

This is for the implementation repo not the demo/tck one

### Request Header

This recording https://raw.githubusercontent.com/servirtium/README/master/broken_recordings/request_body_that_never_happened 
claims to be a recording of https://www.example.com/ but it is not.  Your test should fail because there were unexpected headers in the request.

You are going to remove everything from request headers apart from:


