# Step 7. Other HTTP verbs other than 'GET'

POST, PUT, HEAD, DELETE, OPTIONS, TRACE and PATCH are needed too. Unlike GET, they have a request body, 
but that is pretty much the only difference. Maybe just do unit tests for these, as the extracted 
library's build shouldn't be dependent on remote services.

Some HTTP socket-listener libraries don't have a generic handler for all verbs, and instead have specific 
onGET & onPOST style methods/functionals. Meaning there's a little more copy/paste than you'd wish for.

This step is on the library only, not the demo-xxx-climate-tck repo, which still has 18 tests (6 direct, 6 for record mode, and 6 for playback - all of those using GET).
