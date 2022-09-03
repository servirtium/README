# Step 6. Extract the library from the climate demo, to its own repo

This is so that others could use the library. The demo project needs to be able to "require" the bew Servirtium 
package, of course. The workdbank service tests should stay with the `demo-Xxxxxx-climate-tck` 
repo. Indeed, the new library repo/module tests should not reference WorldBank climate web-API at all. New "pure unit tests" 
could be a good idea at this stage (no I/O) - in the new library repo = hard code fragments of markdown for the sake of tests.

The `demo-Xxxxxx-climate-tck` project still has 18 tests (6 direct, 6 for record mode, and 6 for playback)

Warning: Not all languages make it easy for one project to depend on another that is not yet publish to a binary repository online.
