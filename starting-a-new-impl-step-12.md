# Step 11. Optional Markdown Settings

## Alternate code block

The three backtick way of marking code blocks in markdown, has an alternate: indented by four spaces. That should be supported too - and should be an option in recording mode, with playback mode just adapting to what it encounters. A method/function on the recorder could be `indentCodeBlocks()` whatever is idiomatic for the style of API you are building.

## Emphasis for HTTP verb/method

GET and POST may be in the markdown as emphasised like *GET* or *POST* (asterisk or underscore before & after the word in the markdown). This should be optional too via a recorder method like `emphasizeHttpVerbs()` (or similar). The Playback mode should just adapt to what it encounters, without an explicit method call. 
