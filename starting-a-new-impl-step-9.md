# Step 9. Add a capability for a "Note".

The test code a user would write should be able to add a note for the next interaction, which will appear in the markdown. It is a record-only thing as playback ignores it. This serves as a rudimentary comment system for 
HUMANS (though somebody's bound to try to put YAML in there at some point):

```
...
## Interaction 0: POST /a/b/c

## [Note] Mary:

Mary had a little lamb,
   Its fleece was white as snow,
And every where that Mary went
   The lamb was sure to go ;

### Request headers recorded for playback:
...

```