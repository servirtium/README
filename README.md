# What is Servirtium?

Servirtium is an attempt to evolve **a standard for recorded HTTP conversations is Markdown** to test-automation purposes. Conversations 
would be replayable from the same Markdown format. Multiple language implementations would be able work with the same Markdown 
standard, and it would be possible to record a HTTP conversation with (say) a Ruby library using Test::Unit and the play them back via a (say) Java library for JUnit/TestNG teams.  That would be for the situation where the Ruby team was publishing an API and bundled unit tests with it, but the consuming team was using Java instead of Ruby.

# Example of Markdown format

Here's a screenshot of some raw markdown source:

![2019-10-30_0559](https://user-images.githubusercontent.com/82182/67832718-7092e380-fada-11e9-94a8-58dcc82810cb.png)

(non-screenshot actual source: [https://raw.githubusercontent.com/servirtium/README/master/example1.md](https://raw.githubusercontent.com/servirtium/README/master/example1.md))

Here's what GitHub (for one) renders that like:

![2019-10-30_0555](https://user-images.githubusercontent.com/82182/67832562-f2ced800-fad9-11e9-9bbf-8a366ad7c938.png)

That's the whole point of this format that's human inspectable in raw form and that your code-portal renders in a pretty way too.

(non-screenshot actual rendered file: [https://github.com/servirtium/README/blob/master/example1.md](https://github.com/servirtium/README/blob/master/example1.md))

## Markdown Syntax Explained

### Multiple Interactions Catered For

Each interaction is denoted via a **Level 2 Markdown Heading**. e.g. `## Interaction N: <METHOD> <PATH-FROM-ROOT>`

N starts as 0, and goes up depending on how many interactions there were in the conversation.

<METHOD> is GET or POST (or any standard HTML or non stanard method name).
  
<PATH-FROM-ROOT> is the path without the domain & port. e.g. /card/addTo.doIt  

### Request And Reply Details Per Interaction

Each interaction has four sections denoted by a **Level 3 Markdown headers*

1. The request headers going from the client to the HTTP server, denoted like so `### Request headers recorded for playback:`
2. The request body going from the client to the HTTP server (if applicable - GET does not use this), denoted like so `### Request body recorded for playback (<MIME-TYPE>):`
3. The response headers coming back from the HTTP server to the clent, denoted like so `### Response headers recorded for playback:`
4. The response body coming back from the HTTP server to the clent (some HTTP methods do not use this), denoted like so `### Response body recorded for playback (<STATUS-CODE>: <MINE-TYPE>):`

Within each of those there is a single Markdown code block (three backtick sequences) with the details of each.  The lines in that 
block may be reformatted depending on the settings of the recorder. If binary, then there is a Base64 
sequence instead (admittedly not so pretty on the eye).

# The Contract That Is Tested During Playback

Playback itself should fail if the headers or body sent by the client to the HTTPServer (through the Servirtium library)
are not the same versus the recording. It is possible that masking/redacting and general manipulations may have happened
deliberately during the recording so that to get rid of transient aspects that are not helpful in playback situatons.
For example any Dates in headers of the body that go from the client to the HTTP Server could be swapped for some date 
in the future like "2099-01-01" or a date in the past "1970-01-01". That's up to the person who's designing the tests 
that do he recording and confirming that the same tests in playback mode do the same thing.  If, after that work,
the request headers or body are different in playback mode, the library should cause the playback to fail. That failure
being deliberate should be explicit somehow in the log of the unit test framework. This is easier said that done as it
could be that the playback technology is on a different thread to the test executor.

# Implementations

1. Java - [Servirtium-Java](https://github.com/servirtium/servirtium-java) (in this org) - ready to use
2. Python - Being developed story by story as part of demo [demo-python-climate-data-tck](https://github.com/servirtium/demo-python-climate-data-tck) and will be extracted to its own library/repo at some point
3. Ruby - People wishing to lead development sought.
4. Go - People wishing to lead development sought.
5. C# - People wishing to lead development sought.
6. Node.JS - People wishing to lead development sought.

We're also looking to existing Service Virtualiztion frameworks/libs to support (and help refine) the same Markdown format.

# Demo Projects

1. Java - [demo-java-climate-data-tck](https://github.com/servirtium/demo-java-climate-data-tck)
2. Python - [demo-python-climate-data-tck](https://github.com/servirtium/demo-python-climate-data-tck)
