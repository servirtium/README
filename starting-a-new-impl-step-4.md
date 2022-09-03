# Step 4. Make the recording of a test fail if it is different to what it was previously.

Store the whole recording previously made for each test. When the test completes, check if the whole recording is different and **fail the test** if it is. Just do this in memory and as each test executes. 

```
test:  
    as it is now - calling the climate API for average rainfall with parameters
after-test or tearDown:
    servirtiumRecorder.failIfMarkdownIsDifferentToPreviousRecording()
```

If there are no prior recording, skip this step and just write the markdown to the file system (no test failure)

If it is determined that the recording is different to before, write the recording out to the markdown anyway, even if the test fails. A developer seeing that the test has failed for a clear reason, may want to do `git diff` on their local workstation to see more information, and how to fix it or report root cause problems.

## Diagram of components/services

![image](https://user-images.githubusercontent.com/82182/91491233-a7c55300-e8ab-11ea-95b7-a6884f393cef.png)

