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

## Diagram of components/services

![image](https://user-images.githubusercontent.com/82182/91492094-ed365000-e8ac-11ea-908b-41908bded2a6.png)

### Mutation of Caller Request

![image](https://user-images.githubusercontent.com/82182/91492226-34244580-e8ad-11ea-8377-6273b112194f.png)

Perhaps: 

```
servirtium.recorderMuutations().callerRequest().addReplacement(fromRegex, To)
servirtium.recorderMuutations().callerRequest().addHeaderRemoval(headerNameRegex)
```

Or 

```
servirtium.mutations().addReplacement(RECORDING_CALLER_REQUEST, fromRegex, To)
servirtium.mutations().addHeaderRemoval(RECORDING_CALLER_REQUEST, headerNameRegex)
```

### Mutation of Real Response

![image](https://user-images.githubusercontent.com/82182/91492667-ed831b00-e8ad-11ea-9de1-34bce1e12ae7.png)

Perhaps: 

```
servirtium.recorderMuutations().realResponse().addReplacement(fromRegex, To)
servirtium.recorderMuutations().realResponse().addHeaderRemoval(headerNameRegex)
```

Or 

```
servirtium.mutations().addReplacement(RECORDING_REAL_RESPONSE, fromRegex, To)
servirtium.mutations().addHeaderRemoval(RECORDING_REAL_RESPONSE, headerNameRegex)
```

### Mutation of Real Response

While the "real" needed real passwords and user IDs to function, playback does not. So "Authorization: <real details>" could be replacd with "Authorization: DUMMY_AUTH" and people who value you playback only don't care.

![image](https://user-images.githubusercontent.com/82182/91493326-0e983b80-e8af-11ea-8cbc-91f959cc2d4f.png)

Perhaps: 

```
servirtium.recorderMuutations().recordedResponse().addReplacement(fromRegex, To)
servirtium.recorderMuutations().recordedResponse().addHeaderRemoval(headerNameRegex)
```

Or 

```
servirtium.mutations().addReplacement(RECORDED_RESPONSE, fromRegex, To)
servirtium.mutations().addHeaderRemoval(RECORDED_RESPONSE, headerNameRegex)
```
