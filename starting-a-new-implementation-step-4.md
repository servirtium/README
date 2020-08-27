## 4. Make the recording of a test fail if it is different to what it was previously.

Store the whole recording previously made for each test. When the test completes, check if the whole recording is different and **fail the test** if it is. Just do this in memory and as each test executes. 

```
test:  
    as it is now - calling the climate API for average rainfall with parameters
after-test or tearDown:
    servirtiumRecorder.failIfMarkdownIsDifferentToPreviousRecording()
```

If thee no prior recording, skip this step and just write the markdown to the file system.

