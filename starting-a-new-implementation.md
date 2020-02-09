# General Architecture

You're going to need a `Recorder` (to the markdown format), a `replayer` (from the markdown format), a `server` that can listen on a 
socket and work with the recorder or replayer. In the case of the replayer, the incoming requests are sent to the 'real' service too. 
In the case of the replayer, the "real service" is not involved.  

# How to start new language implementation

This is the suggested way of building Servirtium for a new language as it is methodical. That's useful because you may 
have to pause your development of this and restart later.

Steps:

## 1. Start with an implementation of "direct" with tests

Here's the the "direct" tests you want to (from the Python testbase):

![image](tests.png)

(Source for that: https://github.com/servirtium/demo-python-climate-tck/blob/master/src/test/TestClimateApi.py)

And the URLs you're trying to hit is `http://climatedataapi.worldbank.org/climateweb/rest/v1/country/annualavg/pr/{fromCCYY}/{toCCYY}/{countryISO}.xml`. 

## 2. Implement the "playback" for the same test cases
 
[See PlaybackClimateApiTests.java](https://github.com/servirtium/demo-java-climate-tck/blob/master/src/test/java/com/paulhammant/climatedata/PlaybackClimateApiTests.java) and the mocks that it uses for playback [in here](https://github.com/servirtium/demo-java-climate-tck/tree/master/src/test/mocks). In the Java version PlaybackClimateApiTests is a subclass of ClimateApiTests, but you may want to achieve the same thing in a different way.  This creates your fledgeling Servirtium.

To be clear, the same tests have the ability to pass in "direct" (no Servirtium) and "playback" modes of operation.

Also of note that Servirtium's playback server is a deliberate man-in-the-middle - meaning that the climate-lib needs to invoke 
services on http://localhost:61417/climateweb/rest/v1/ instead of http://climatedataapi.worldbank.org/climateweb/rest/v1/

## 3. Adding "record" mode

You should have the hang of this now :)

[See RecordingClimateApiTests.java](https://github.com/servirtium/demo-java-climate-tck/blob/master/src/test/java/com/paulhammant/climatedata/RecordingClimateApiTests.java) - this (a subclass again) adds tests recording mode for the Servirtium for the same test cases.
mow

To be clear, the same tests have the ability to pass in "direct" (no Servirtium), "playback", and "record" modes of operation

Success is where the recording doesn't change regardless of how many time you run the tests (overwriting the .md files in tests/mocks/ (or whatever you have as that directory in Git)

## 4. Add second and subsequent interaction handling

For direct tests (as well as Servirtium record and playback), add the possibility of calculating averages for more than one 
country code. Here's the Python test for that.

![image](gbr-fra.png)

Yes, the 'gbr+fra' test hits the HTTP api twice (yes that breaks the facade pattern, but this is just a test harness for Servirtium).

## 5. Extract the library from the climate demo, to its own repo

This is so that others could use the library. The demo project needs to be able to acquire the package, of course.  Pure unit tests
could be a good idea at this stage, as the climate tests are integration/service tests.

## 6. Other HTTP verbs other than 'GET'

POST, PUT are needed too - unlike GET they have a request body. Maybe just do unit tests for this, as the library's build shouldn't be
overly dependant on remote services.

## 7. Add a capability for a "Note".

The testing tech, can add a note for the next interaction, which will appear in the markdown. It's a record only thing as Playback 
ignores it. This serves as a rudimentary comment system for HUMANS (though somebody's bound to try to put YAML in there at some point):

```
## Interaction 0: POST /a/b/c

## [Note] Mary:

Mary had a little lamb,
   Its fleece was white as snow,
And every where that Mary went
   The lamb was sure to go ;

### Request headers recorded for playback:
```

## 8. Redaction / Mask / Mutate operations

Sometimes things have to be changed in request headers and/or request body that is saved as markdown in a recording
Similarly things may have to be changed in response headers and/or response body.  

Related things that were recorded in a certain way, may have to be changed again in playback. You might have morphed 
`Date: Wed, 21 Oct 2019 07:28:00 GMT` to `Date: todays's-date-paul-was-here` for the purposes of the recording, but
in playback it needs to be changed again from `Date: todays's-date-paul-was-here` to `Date: Sun, 9 Feb 2020 11:18:03 GMT` 
so that tests still pass.

Then there's also removal of headers (and parts of a body) at both request and response level, that's needed.

For any of these it may be a good idea to get regex and non regex ways working.

## 9. Proxy Server mode of operation

This one varies per language and the HTTP request initiation available. Client calls to an arbitrary server, can be run through 
a proxy server on the way there. Some commercial Service Virtualization techs like HoverFly work this way by design. For Servirtium 
it is an option.  If mounted as a Proxy Server technologies that would call over the wire may not be specifically configured 
for it.

# Prior implementations

# Java using Netty, Undertow and OKHttp libraries.

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

