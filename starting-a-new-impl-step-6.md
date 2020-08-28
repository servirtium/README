# Step 6. Extract the library from the climate demo, to its own repo

This is so that others could use the library. The demo project needs to be able to acquire the 
package, of course. The workdbank service tests should stay with the `demo-xxx-climate-tck` 
repo. Indeed, the library tests should not reference WorldBank climate web-API at all. New "pure unit tests" 
could be a good idea at this stage (no I/O) - in the new library repo.

The `demo-xxx-climate-tck` project still has 18 tests (6 direct, 6 for record mode, and 6 for playback)
