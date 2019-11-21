# General Architecture

Here's a class diagram for Java implementation.

![the class diagram](servirtium-java-class-diagram.png)

You'd only copy that if it makes sense for your language. That's because doing things in an idiomatically 
correct way for your language could mean something very different.  

So in the first Java implementation, there's a 
`Recorder` or `playback` that works in conjunction with a `Servirtium Server` which listens on a socket an is
a "man in the middle". That last has a dependency on Jetty or Undertow (two alternate implemenations) 
Alternates in Java could be Jetty or Tomcat. All of those 
are open source web servers. There's one built into to later versions of Java, so that could be another
alternate one day. Ruby and Python had built-in web servers far sooner than Java did, so that'll be less dramatic.

Similarly, outgoing HTP requests in the Java solution is via the open source component OkHttp. Later versions 
of java build that in so at some point there'll be a implementation that does that.

Really though, Jetty and OkHttp are decent choices for this tech as it is **test time only**. Nobody's production
system will depend on this. We need functional correctness, error resilience but not million-requests a second 
scale. 

# "Baby Steps" for a new language implementation

1. Start with an implementation of "direct" for the test cases in the Java demo that utilizes the World-Bank's Climate API - [see ClimateApiTests.java](https://github.com/servirtium/demo-java-climate-data-tck/blob/master/src/test/java/com/paulhammant/climatedata/ClimateApiTests.java). Not JUnit for your language, obviously, but PyTest, RSpec, Jasmine, NUnit (etc) instead. 
2. Then implement the "playback" for the test cases in same Java demo - [see PlaybackClimateApiTests.java](https://github.com/servirtium/demo-java-climate-data-tck/blob/master/src/test/java/com/paulhammant/climatedata/PlaybackClimateApiTests.java) and the mocks that it uses for playback - [see mocks/](https://github.com/servirtium/demo-java-climate-data-tck/tree/master/src/test/mocks)
3. You should have the hang of this mow - move on to record
4. Now think about the other HTTP verbs other than 'GET'

