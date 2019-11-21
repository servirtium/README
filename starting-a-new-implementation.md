# General Architecture

Here's [the class diagram](servirtium-java-class-diagram.png) of Java implementation.

You'd only copy that if it makes sense for your language. That's because doing things in an idiomatically 
correct way for your language could mean something very differently.

# Baby Steps

1. Start with an implementation of "direct" for the test cases in the Java demo ([see ClimateApiTests.java](https://github.com/servirtium/demo-java-climate-data-tck/blob/master/src/test/java/com/paulhammant/climatedata/ClimateApiTests.java)) that utilizes the World-Bank's Climate API
2. Then implement the "playback" for the test cases in same Java demo - [see PlaybackClimateApiTests.java](https://github.com/servirtium/demo-java-climate-data-tck/blob/master/src/test/java/com/paulhammant/climatedata/PlaybackClimateApiTests.java) and the mocks that it uses for playback - [see mocks/](https://github.com/servirtium/demo-java-climate-data-tck/tree/master/src/test/mocks)
3. You should have the hang of this mow - move on to record
4. Now think about the other HTTP verbs other than 'GET'

