# Step 3. Adding "record" mode to what you have

You should have the hang of this now :)

[See RecordingClimateApiTests.java](https://github.com/servirtium/demo-java-climate-tck/blob/master/src/test/java/com/paulhammant/climatedata/RecordingClimateApiTests.java) - 

See [TestRecordingClimateApi.py](https://github.com/servirtium/demo-python-climate-tck/blob/master/src/test/TestRecordingClimateApi.py) - this adds tests recording mode for the Servirtium for the same test cases. 

To be clear, the same tests have now the ability to pass in "direct" (no Servirtium), "playback", 
and "record" modes of operation.  You should think about the right way of command-line subsetting 
to the same class, as IDE operation for a single test is not enough.

Success is where the recording doesn't change regardless of how many times you run the tests 
(overwriting the .md files in tests/mocks/ (or whatever you have as that directory in Git)

Note that Servirtium's recording server is a deliberate middleware - meaning that the 
climate-lib needs to invoke services on http://localhost:61417/climateweb/rest/v1/ (or http://servirtium.local.gd:61417 for additional clarity)
instead of ~~http://climatedataapi.worldbank.org/climateweb/rest/v1/~~ https://servirtium.github.io/worldbank-climate-recordings/climateweb/rest/v1/. Specifically, the climate API test-harness 
needs to be configurable to choose the base domain name / port. A constructor arg is a good way to specify that, 
but language idioms differ. 

<img src="https://raw.github.com/servirtium/README/master/3.svg?sanitize=true">

## Diagram of components/services

![image](https://user-images.githubusercontent.com/82182/91487112-2c60a300-e8a5-11ea-8e3d-1311925b25c7.png)

