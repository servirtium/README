# Step 3. Adding "record" mode to what you have

You should have the hang of this now :)

[See RecordingClimateApiTests.java](https://github.com/servirtium/demo-java-climate-tck/blob/master/src/test/java/com/paulhammant/climatedata/RecordingClimateApiTests.java) - this (a subclass again) adds tests recording mode for the Servirtium for the same test cases.
mow

To be clear, the same tests have the ability to pass in "direct" (no Servirtium), "playback", 
and "record" modes of operation.

Success is where the recording doesn't change regardless of how many time you run the tests 
(overwriting the .md files in tests/mocks/ (or whatever you have as that directory in Git)

Note that Servirtium's record server is a deliberate man-in-the-middle - meaning that the 
climate-lib needs to invoke services on http://localhost:61417/climateweb/rest/v1/ (or http://servirtium.local.gd:61417 for additional clarity)
instead of http://climatedataapi.worldbank.org/climateweb/rest/v1/. Specifically, the climate API test-harness 
needs to be configurable to choose the base domain name / port. A constructor arg is a good way to specify that, 
but language idioms differ.

<img src="https://raw.github.com/servirtium/README/master/3.svg?sanitize=true">

## Diagram of components/services

![image](https://user-images.githubusercontent.com/82182/91487112-2c60a300-e8a5-11ea-8e3d-1311925b25c7.png)

