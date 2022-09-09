# Step 8. Mutation operations (Redaction, Mask, Delete)

Sometimes things have to be changed in request headers and/or request body that is saved as markdown in a recording. Similarly, things may have to be changed in response headers and/or response body.  

Related things that were recorded in a certain way, may have to be changed again in playback. You might have morphed `Date: Wed, 21 Oct 2019 07:28:00 GMT` to `Date: todays's-date-paul-was-here` for the purposes of the recording, but in playback it needs to be changed again from `Date: todays's-date-paul-was-here` to `Date: Sun, 9 Feb 2020 11:18:03 GMT` so that tests still pass.

Then there's also removal of headers (and parts of a body) at both request and response level, that's needed.

For any of these it may be a good idea to get regex and non regex ways working.

You'll note that the recording generates many differences between recordings (back to back). That is a good list of things to check off for mutation, mask, redaction, deletion.

You'll also note that some of the same Redaction, Mask, Delete, and Mutate operations should be in playback. Or perhaps: un_redact, un_mask, un_mutate.

## Diagram of components/services

![image](https://user-images.githubusercontent.com/82182/91542257-741f1300-e915-11ea-9e25-13ebe633e2ba.png)

### 8.1 Recorder: Mutation of Caller Request

![image](https://user-images.githubusercontent.com/82182/91541961-01159c80-e915-11ea-80ba-1872b61c57e0.png)

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

### 8.2 Recorder: Mutation of Real Response

![image](https://user-images.githubusercontent.com/82182/91542012-17bbf380-e915-11ea-95a8-7237c971b0f9.png)

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


### 8.3 Recorder: Further Mutation of Caller Request For Recording

While the "real" needed real passwords and user IDs to function, playback does not ad we should never share secrets - not even for pre-prod infrastructure. So "Authorization: <real details>" could be replaced with "Authorization: DUMMY_AUTH" and devs who value playback only don't care that the authorization is dummy for some functional interaction.

![image](https://user-images.githubusercontent.com/82182/91542052-27d3d300-e915-11ea-85e2-ee5bd73c5be7.png)

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


### 8.4 Recorder: Further Mutation of Real Response For Caller

This would be used to turn:

* `Date: DUMMY_day-name,day_month_year_hour:minute:secon_TZ` back into `Date: Wed, 21 Oct 2015 07:28:00 GMT` for the caller (if needed).
* `realdomain.com` back into `localhost:61417` for the caller (most web-APIs don't put long URLs in response bodies, but WorldBank's climate API does).

![image](https://user-images.githubusercontent.com/82182/91542121-40dc8400-e915-11ea-9c23-09a6fe1a8dee.png)

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


### 8.5 Playback: Mutation of Caller Request

![image](https://user-images.githubusercontent.com/82182/91542175-5487ea80-e915-11ea-9fec-47ceafeef07b.png)

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


### 8.6 Playback: Further Mutation of Real Response For Caller

This would be used to turn:

* `Date: DUMMY_day-name,day_month_year_hour:minute:secon_TZ` back into `Date: Wed, 21 Oct 2015 07:28:00 GMT` for the caller (if needed).
* `realdomain.com` back into `localhost:61417` for the caller (most web-APIs don't put long URLs in response bodies, but WorldBank's climate API does).

![image](https://user-images.githubusercontent.com/82182/91542218-65d0f700-e915-11ea-8bb4-d5e3dd953867.png)

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

## Applicability to WorldBank's climate web-API

### 8.1 Recorder: Mutation of Caller Request

As middleware, Servirtium will receive GETs, POSTs and more with localhost:61417 and http://localhost:61417 in the headers and bodies of REQUESTS. The read web-API (http://climatedataapi.worldbank.org - port 80) can't have "localhost" going up to it at all.

Thus:

* All references to http://localhost:61417 in request bodies need to be changed to http://climatedataapi.worldbank.org
* A reference to localhost:61417 in the "host" request header needs to be changed to climatedataapi.worldbank.org

### 8.2 Recorder: Mutation of Real Response

Most likely there are no mutations needed to the REAL response before it is saved as markdown (for future playback)

### 8.3 Recorder: Further Mutation of Caller Request For Recording

Most likely there are no mutations needed to the REAL response before it is saved as markdown (for future playback)

### 8.4 Recorder: Further Mutation of Real Response For Caller

* All references to http://climatedataapi.worldbank.org in response bodies need to be changed to http://localhost:61417 before replying to the caller.
* A reference to localhost:61417 in the "location" response header needs to be changed to climatedataapi.worldbank.org without changing the rest of the URL.

### 8.5 Playback: Mutation of Caller Request

As 8.1, but it isn't always going to be the case, so 8.1 and 8.5 need to be handled separately.

### 8.6 Playback: Further Mutation of Real Response For Caller

As 8.2, but it isn't always going to be the case, so 8.2 and 8.6 need to be handled separately.

