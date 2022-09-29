Main Servirtium site: https://servirtium.dev

# General Architecture

You're going to need a `Recorder` (to the markdown format), a `replayer` (from the markdown format), a `server` that can listen on a socket and work with the recorder or replayer. In the case of the recorder ("man in the middle"), the incoming requests are sent to the 'real' service too. 
In the case of the replayer, the "real service" is not involved.  

# How to start new language implementation

This is the suggested way of building Servirtium for a new language as it is methodical. That's useful because you may have to pause your development of this and restart later. So we're going to this in many small steps. The first isn't even about Servirtium at all.  

Methodical is the idea here.  This is all pausable/resumable as an activity. Indeed Fred and Wilma can pair on step 1, get busy on other important things, then Betty and Barney can pick up step 2 (from what was checked in) and continue.

**Steps:**

1. [Write a simple API class with tests](starting-a-new-impl-step-1.md)
2. [Implement a rudimentary "playback" for the same test cases](starting-a-new-impl-step-2.md)
3. [Adding "record" mode to what you have](starting-a-new-impl-step-3.md)
4. [Make the recording of a test fail if it is different to what it was previously](starting-a-new-impl-step-4.md)
5. [Add second and subsequent interaction handling](starting-a-new-impl-step-5.md)
6. [Extract the library from the climate demo, to its own repo](starting-a-new-impl-step-6.md)
7. [Other HTTP verbs other than 'GET'](starting-a-new-impl-step-7.md)
8. [Mutation operations (Redaction, Mask, Delete)](starting-a-new-impl-step-8.md)
9. [Add a capability for a "Note"](starting-a-new-impl-step-9.md)
10. [Fail a playback step if the request is not as previously recorded](starting-a-new-impl-step-10.md)
11. [Optional Markdown Settings](starting-a-new-impl-step-11.md)
12. [Publish to package/module-land for your language family](starting-a-new-impl-step-12.md)
13. [Proxy Server mode of operation](starting-a-new-impl-step-13.md)
14. [Pass the compatibility suite](starting-a-new-impl-step-14.md)

# Notes on prior implementations

If you're making a new impl, you don't actually have to understand the architecture of previous implementations. Indeed, your impl may be better for **not** being educated on prior implementations.

* Here's the [Kotlin API of step 1](https://github.com/http4k/servirtium-demo-kotlin-climate-tck/blob/master/src/main/kotlin/servirtium/http4k/ClimateApi.kt), and the JUnit5 [tests for that](https://github.com/http4k/servirtium-demo-kotlin-climate-tck/blob/master/src/test/kotlin/servirtium/http4k/kotlin/ClimateApiTests.kt). 
