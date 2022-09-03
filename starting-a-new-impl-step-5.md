# Step 5. Add second and subsequent interaction handling

Each of the five tests done **so far** in the climate-api took a single country code.

Change: For **direct mode** tests (as well as Servirtium **record** and **playback** modes), add the possibility of calculating rainfall averages for more than one 
country code (changes in our test harness). That would be a list of countries. Here's the Python test for for a new test for 'gbr' and 'fra' rainfall average (pseudo code again):

```
test_averageRainfallForGreatBritainAndFranceFrom1980to1999CanBeCalculatedFromTwoRequests()
    assert climateApi.getAveAnnualRainfall(1980, 1999, "gbr", "fra") == 951.3220963726872
```

Yes, the 'gbr+fra' test hits the WordBank climate web-api twice. Yes, that breaks the facade pattern, but this is 
just a **test harness** for Servirtium.

In the Markdown grammar, there's an interaction number that shows the order of the **TWO** interactions (one for 'gbr' and one for 'fra')

```
## Interaction 0: GET /climateweb/rest/v1/country/annualavg/pr/1980/1999/gbr.xml
   
   ... sections for: request headers, request body, response headers, response body ...
   
## Interaction 1: GET /climateweb/rest/v1/country/annualavg/pr/1980/1999/fra.xml
   
   ... sections for: request headers, request body, response headers, response body ... 
   
```

**Most likely your well-factored code makes it easy to record a series of interactions.**

There now should be 18 tests: 6 direct, 6 for record mode, and 6 for playback. Shared code should be a reality - ideally all the tests are written once and used three times (direct, record, and playback modes).
