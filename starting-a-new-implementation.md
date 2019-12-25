# General Architecture

Here's a class diagram for Java implementation.

![the class diagram](servirtium-java-class-diagram.png)

You'd only copy that if it makes sense for your language. That's because doing things in an idiomatically 
correct way for your language could mean something very different. The Python version of Servertium is much more 
pythonic than the class-centric Java version.

So in the first Java implementation, there's a 
`Recorder` or `playback` that works in conjunction with a `Servirtium Server` which listens on a socket an is
a "man in the middle". That last has a dependency on Jetty or Undertow (two alternate implementations) 
Alternates in Java could be Jetty or Tomcat. All of those 
are open source web servers. There's one built into to later versions of Java, so that could be another
alternate one day. Ruby and Python had built-in web servers far sooner than Java did, so that'll be less dramatic.

Similarly, outgoing HTP requests in the Java solution is via the open source component OkHttp. Later versions 
of java build that in so at some point there'll be a implementation that does that.

Really though, Jetty and OkHttp are decent choices for this tech as it is **test time only**. Nobody's production
system will depend on this. We need functional correctness, error resilience but not million-requests a second 
scale. 

# "Baby Steps" for a new language implementation

## 1. Start with an implementation of "direct" with tests
 
In the Java demo that utilizes the World-Bank's Climate API [take a look at ClimateApiTests.java](https://github.com/servirtium/demo-java-climate-data-tck/blob/master/src/test/java/com/paulhammant/climatedata/ClimateApiTests.java). Obviously not JUnit for your language, but PyTest, RSpec, Jasmine, NUnit (etc) instead. 

## 2. Implement the "playback" for the same test cases
 
[See PlaybackClimateApiTests.java](https://github.com/servirtium/demo-java-climate-data-tck/blob/master/src/test/java/com/paulhammant/climatedata/PlaybackClimateApiTests.java) and the mocks that it uses for playback [in here](https://github.com/servirtium/demo-java-climate-data-tck/tree/master/src/test/mocks). In the Java version PlaybackClimateApiTests is a subclass of ClimateApiTests, but you may want to achieve the same thing in a different way.  This creates your fledgeling Servirtium.

## 3. You should have the hang of this mow - move on to record

[See RecordingClimateApiTests.java](https://github.com/servirtium/demo-java-climate-data-tck/blob/master/src/test/java/com/paulhammant/climatedata/RecordingClimateApiTests.java) - this (a subclass again) adds tests recording mode for the Servirtium for the same test cases.

## 4. Now think about the other HTTP verbs other than 'GET'

