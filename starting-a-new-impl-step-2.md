# Step 2. Implement a rudimentary "playback" for the same test cases

**This step creates a fledgling Servirtium**

A playback Servirtium (in the test-base) should be able to respond as the WorldBank's climate web-api would for the same calls, and the new (derived or extended) tests should work offline just fine.

See [see TestPlaybackClimateApi.py](https://github.com/servirtium/demo-python-climate-tck/blob/master/src/test/TestPlaybackClimateApi.py) and the mocks that it uses for playback [in here](https://github.com/servirtium/demo-python-climate-tck/tree/master/src/mocks). The content of mocks for the Python version should be the same as the content for the Java version, even if the file names/paths are slightly different. Those mocks are checked into source-control alongside the tests, without being modified.

Parsing of the markdown files **is easy**. Uses your language's regex. A markdown file has a series of interactions. They are separated like so `"\n## Interaction "` (markdown's heading-level-2 macro). Within each interactiion there are four sections separated like so `"\n### "` (markdown's heading-level-3 macro). Within each of those there is a code block with `"\n```\n"` (code fence in markdown lingo). It's just a job of nesting some for looks to turn the markdown into something that programatic use during replay. 

To be clear, the same five tests you already have the ability to pass in "direct" (no Servirtium) **and** "playback" modes of operation. And these two sets of five **should** share code as much as possible (code reuse, test inheritance or composition - are both good). Ten tests in all.

Note too, that in order to stay "in process" with this step you're going to have to leverage 
some multi-threading or async capability to allow a test suite to issue GETs through the HTTP client library you have chosen and simultaneously some HTTP "servirtium server" to listen on a socket to satisfy that GET. Constraint is: no process spawning. The Go implementation does a "Go Routine" which is idiomatic for that world, but again that is not a process.

<img src="https://raw.github.com/servirtium/README/master/2.svg?sanitize=true">

Notes:
1. The server you're standing up should not have an SSL certificate or speak over HTTPS. It would be `localhost:61417` by convention, but you could specify `servirtium.local.gd:61417` if you wanted for additional clarity for the casual code reader. Read about [local.gd](http://local.gd).

2. In the event of Servirtium issuing errors/exceptions during interactions, your fledgling Servirtium should provide a mechanism for the test runner to find out what failed in the last interaction:  `servirtium.GetLastError()`. Depending on what is idiomatic for the test runner/language that could be in a try/catch block or a "tear down" or "after". Either way it should be programmatic. 



## Diagram of components/services

![image](https://user-images.githubusercontent.com/82182/91485984-8a8c8680-e8a3-11ea-9b9e-bdefd657452d.png)

Yes, Worldbank's web-API isn't involved in this step - the five new tests won't cause I/O to Worldbank.
