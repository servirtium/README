# What is Servirtium

Servirtium is an attempt to evolve a standard for recorded HTTP conversations is Markdown to test-automation purposes. Conversations 
would be replayable from the same Markdown format. Multiple language implementations would be able work with the same Markdown 
standard, and it would be possible to record a HTTP conversation with (say) a Ruby library using Test::Unit and the play them back via a (say) Java library for JUnit/TestNG teams.  That would be for the situation where the Ruby team was publishing an API and bundled unit tests with it, but the consuming team was using Java instead of Ruby.

# Example of Markdown format

Here's a screenshot of some raw markdown source:

![2019-10-30_0559](https://user-images.githubusercontent.com/82182/67832718-7092e380-fada-11e9-94a8-58dcc82810cb.png)

(non-screenshot actual source: [https://raw.githubusercontent.com/servirtium/README/master/example1.md](https://raw.githubusercontent.com/servirtium/README/master/example1.md))

Here's what GitHub (for one) renders that like:

![2019-10-30_0555](https://user-images.githubusercontent.com/82182/67832562-f2ced800-fad9-11e9-9bbf-8a366ad7c938.png)

That's the whole point of this format that's human inspectable in raw form and that your code-portal renders in a pretty way too.

(non-screenshot actual rendered file: [https://raw.githubusercontent.com/servirtium/README/master/example1.md](https://raw.githubusercontent.com/servirtium/README/master/example1.md))
