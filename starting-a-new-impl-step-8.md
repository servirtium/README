# Step 8. Mutation operations (Redaction, Mask, Delete)

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

### Recorder: Mutation of Caller Request

![image](https://user-images.githubusercontent.com/82182/91492226-34244580-e8ad-11ea-8377-6273b112194f.png)

Perhaps: 

```
servirtium.recorderMutations().callerRequest().addReplacement(fromRegex, To)
servirtium.recorderMutations().callerRequest().addHeaderRemoval(headerNameRegex)
```

Or:

```
servirtium.mutations().addReplacement(RECORDING_CALLER_REQUEST, fromRegex, To)
servirtium.mutations().addHeaderRemoval(RECORDING_CALLER_REQUEST, headerNameRegex)
```

Maybe: 

```
servirtium.recorder(
   callerRequest( 
     addReplacement(fromRegex, To)
     addHeaderRemoval(headerNameRegex)
   )
)
```

### Recorder: Mutation of Real Response

![image](https://user-images.githubusercontent.com/82182/91492667-ed831b00-e8ad-11ea-9de1-34bce1e12ae7.png)

Perhaps: 

```
servirtium.recorderMutations().realResponse().addReplacement(fromRegex, To)
servirtium.recorderMutations().realResponse().addHeaderRemoval(headerNameRegex)
```

Or:

```
servirtium.mutations().addReplacement(REAL_RESPONSE, fromRegex, To)
servirtium.mutations().addHeaderRemoval(REAL_RESPONSE, headerNameRegex)
```

Maybe: 

```
servirtium.recorder(
   realResponse( 
     addReplacement(fromRegex, To)
     addHeaderRemoval(headerNameRegex)
   )
)
```


### Recorder: Further Mutation of Caller Request For Recording

While the "real" needed real passwords and user IDs to function, playback does not ad we should never share secrets - not even for pre-prod infrastructure. So "Authorization: <real details>" could be replaced with "Authorization: DUMMY_AUTH" and devs who value playback only don't care that the authorization is dummy for some functional interaction.

![image](https://user-images.githubusercontent.com/82182/91493326-0e983b80-e8af-11ea-8cbc-91f959cc2d4f.png)

Perhaps: 

```
servirtium.recorderMutations().recordedRequest().addReplacement(fromRegex, To)
servirtium.recorderMutations().recordedRequest().addHeaderRemoval(headerNameRegex)
```

Or: 

```
servirtium.mutations().addReplacement(RECORDED_REQUEST, fromRegex, To)
servirtium.mutations().addHeaderRemoval(RECORDED_REQUEST, headerNameRegex)
```

Maybe: 

```
servirtium.recorder(
   recordedRequest( 
     addReplacement(fromRegex, To)
     addHeaderRemoval(headerNameRegex)
   )
)
```


### Recorder: Further Mutation of Real Response For Caller

This would be used to turn:

* `Date: DUMMY_day-name,day_month_year_hour:minute:secon_TZ` back into `Date: Wed, 21 Oct 2015 07:28:00 GMT` for the caller (if needed).
* `realdomain.com` back into `localhost:61417` for the caller (most web-APIs don't put long URLs in response bodies, but WorldBank's climate API does).

![image](https://user-images.githubusercontent.com/82182/91523234-1a5a2100-e8f4-11ea-87d0-ea56cc41beb4.png)

Perhaps: 

```
servirtium.recorderMutations().callerResponse().addReplacement(fromRegex, To)
servirtium.recorderMutations().callerResponse().addHeaderRemoval(headerNameRegex)
```

Or: 

```
servirtium.mutations().addReplacement(RECORDING_CALLER_RESPONSE, fromRegex, To)
servirtium.mutations().addHeaderRemoval(RECORDING_CALLER_RESPONSE, headerNameRegex)
```

Maybe: 

```
servirtium.recorder(
   callerResponse( 
     addReplacement(fromRegex, To)
     addHeaderRemoval(headerNameRegex)
   )
)
```


### Playback: Mutation of Caller Request

![image](https://user-images.githubusercontent.com/82182/91523627-272b4480-e8f5-11ea-8c4b-f93eca7a5817.png)

Perhaps: 

```
servirtium.playbackMutations().callerRequest().addReplacement(fromRegex, To)
servirtium.playbackMutations().callerRequest().addHeaderRemoval(headerNameRegex)
```

Or: 

```
servirtium.mutations().addReplacement(PLAYBACK_CALLER_REQUEST, fromRegex, To)
servirtium.mutations().addHeaderRemoval(PLAYBACK_CALLER_REQUEST, headerNameRegex)
```

Maybe: 

```
servirtium.playback(
   callerRequest( 
     addReplacement(fromRegex, To)
     addHeaderRemoval(headerNameRegex)
   )
)
```


### Playback: Further Mutation of Real Response For Caller

This would be used to turn:

* `Date: DUMMY_day-name,day_month_year_hour:minute:secon_TZ` back into `Date: Wed, 21 Oct 2015 07:28:00 GMT` for the caller (if needed).
* `realdomain.com` back into `localhost:61417` for the caller (most web-APIs don't put long URLs in response bodies, but WorldBank's climate API does).

![image](https://user-images.githubusercontent.com/82182/91524140-65753380-e8f6-11ea-9392-6cdc6ad00e37.png)

Perhaps: 

```
servirtium.playbackMutations().callerResponse().addReplacement(fromRegex, To)
servirtium.playbackMutations().callerResponse().addHeaderRemoval(headerNameRegex)
```

Or: 

```
servirtium.mutations().addReplacement(PLAYBACK_CALLER_RESPONSE, fromRegex, To)
servirtium.mutations().addHeaderRemoval(PLAYBACK_CALLER_RESPONSE, headerNameRegex)
```

Maybe: 

```
servirtium.playback(
   callerResponse( 
     addReplacement(fromRegex, To)
     addHeaderRemoval(headerNameRegex)
   )
)
```
