# Step 14. Pass the compatibility suite

This is a more convoluted setup of Selenium and web-app that contains a Mocha test suite. The test suite pre-existed the creation of Servirtium, but serves us well for a larger confirmation of the compatibility of an implementation of Servirtium.

Copy https://github.com/servirtium/servirtium-javascript/blob/master/compatibility-suite.py into your implementation repo.

Then be inspired by the [JavaScript/Node](https://github.com/servirtium/servirtium-javascript/blob/master/src/todobackend_compatibility_test.js) or  [Go](https://github.com/servirtium/servirtium-go/blob/master/cmd/todobackend_compatibility.go) server 'shim' to do record and playback for the 42-interaction compatibility suite.

"Servirtium as a separate server/process" isn't a normal mode of operation for Servirtium. "Servirtium in process" is the normal mode.

Tests you'll want to pass:

## Direct mode:

```
python3 compatibility-suite.py direct
```

This just run's Pete Hodgson's TODO-Backend Mocha suite in a browser against the "real" backend: https://todo-backend-sinatra.herokuapp.com

## Record mode:

```
python3 compatibility-suite.py record
```

This changes to use our fork of Pete's TODO-Backend Mocha suite, and records the 42 interactions via Servirtium

## Playback mode:

```
python3 compatibility-suite.py playback
```

This doesn't need the real backend of course, it uses the recordings from the above.

# Confirming the correctness of everything

We have some sed/awk that attempts to neutralize the inconsequential differences in each recording ...

```
bash <(curl -s https://raw.githubusercontent.com/servirtium/compatibility-suite/master/compare_recording_with_reference_case.sh) path/to/todobackend/recordings.md 
```

... and compare that to a reference recording: https://github.com/servirtium/compatibility-suite/blob/master/todobackend_test_suite_reference.md