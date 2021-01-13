# Step 2. Implement a rudimentary "playback" for the same test cases

**This step creates a fledgling Servirtium**

A playback Servirtium (in the test-base) should be able to respond as the WorkdBank's climate web-api would for the same calls, and the new (derived or extended) tests should work offline just fine.
 
[See PlaybackClimateApiTests.java](https://github.com/servirtium/demo-java-climate-tck/blob/master/src/test/java/com/paulhammant/climatedata/PlaybackClimateApiTests.java) from the Java version and the mocks that it uses for playback [in here](https://github.com/servirtium/demo-java-climate-tck/tree/master/src/test/mocks). In the Java version PlaybackClimateApiTests is a **subclass** of ClimateApiTests, but you may want to achieve the same thing differently (say composition)  

Or [see TestPlaybackClimateApi.py](https://github.com/servirtium/demo-python-climate-tck/blob/master/src/test/TestPlaybackClimateApi.py) and the mocks that it uses for playback [in here](https://github.com/servirtium/demo-python-climate-tck/tree/master/src/mocks). The content of mocks for the Python version should be the same as the content for the Java version, even if the file names/paths are slightly different. An those mocks are checked into source-control alongside the tests, without being modified.

To be clear, the same five tests you already have the ability to pass in "direct" (no Servirtium) **and** "playback" modes of operation. And these two sets of five should share code as much as possible (code reuse, test inheritance or composition - are both good). Ten tests in all.

Note too, that in order to stay "in process" with this step you're going to have to leverage 
some multi-threaded or async capability to allow a test suite to issue GETs through the HTTP client library you have chosen and simultaneously some HTTP "servirtium server" to listen on a socket to satisfy that GET. Constraint is: no process spawning.

<img src="https://raw.github.com/servirtium/README/master/2.svg?sanitize=true">

Notes:
1. The server you're standing up should not have an SSL certificate or speak over HTTPS. 

2. In the event of Servirtium issuing errors/exceptions during interactions, your fledgling Servirtium should provide a mechanism for the test runner to find out what failed in the last interaction. Depending on what is idiomatic for the test runner/language that could be in a try/catch block or a "tear down" or "after". Either way it should be programatic. 

## Diagram of components/services

![image](https://user-images.githubusercontent.com/82182/91485984-8a8c8680-e8a3-11ea-9b9e-bdefd657452d.png)

Yes, Worldbank's web-API isn't involved in this step - the five new tests won't cause I/O to Worldbank.