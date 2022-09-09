# Step 1. Write a simple API class with tests

Here are the tests that you want to pass (pseudo code):

```
test_averageRainfallForGreatBritainFrom1980to1999Exists()
    assert climateApi.getAveAnnualRainfall(1980, 1999, "gbr") == 988.8454972331015

test_averageRainfallForFranceFrom1980to1999Exists()
    assert climateApi.getAveAnnualRainfall(1980, 1999, "fra") == 913.7986955122727

test_averageRainfallForEgyptFrom1980to1999Exists()
    assert climateApi.getAveAnnualRainfall(1980, 1999, "egy") == 54.58587712129825

test_averageRainfallForGreatBritainFrom1985to1995DoesNotExist()
    climateApi.getAveAnnualRainfall(1985, 1995, "gbr")
    ... causes "date range not supported" 

test_averageRainfallForMiddleEarthFrom1980to1999DoesNotExist()
    climateApi.getAveAnnualRainfall(1980, 1999, "mde")
    ... causes "bad country code"
```

And the URLs you're trying to hit is 
`https://servirtium.github.io/worldbank-climate-recordings/climateweb/rest/v1/country/annualavg/pr/{fromCCYY}/{toCCYY}/{countryISO}.xml`. 
Which is a recording of `http://climatedataapi.worldbank.org/climateweb/rest/v1/country/annualavg/pr/{fromCCYY}/{toCCYY}/{countryISO}.xml` (which is down temporarily).

Endpoints we use: [/climateweb/rest/v1/country/annualavg/pr/1980/1999/egy.xml](https://servirtium.github.io/worldbank-climate-recordings/climateweb/rest/v1/country/annualavg/pr/1980/1999/egy.xml), [/climateweb/rest/v1/country/annualavg/pr/1980/1999/fra.xml](https://servirtium.github.io/worldbank-climate-recordings/climateweb/rest/v1/country/annualavg/pr/1980/1999/fra.xml), [/climateweb/rest/v1/country/annualavg/pr/1980/1999/gbr.xml](https://servirtium.github.io/worldbank-climate-recordings/climateweb/rest/v1/country/annualavg/pr/1980/1999/gbr.xml), [/climateweb/rest/v1/country/annualavg/pr/1980/1999/mde.xml](https://servirtium.github.io/worldbank-climate-recordings/climateweb/rest/v1/country/annualavg/pr/1980/1999/mde.xml), [/climateweb/rest/v1/country/annualavg/pr/1985/1995/gbr.xml](https://servirtium.github.io/worldbank-climate-recordings/climateweb/rest/v1/country/annualavg/pr/1985/1995/gbr.xml)

Note that there is nothing of **Servirtium** in this initial step - this is just creation of a "test harness" in your language's preferred test runner (and following best practices including separation of prod code and test code, and a build script if necessary).

<img src="https://raw.github.com/servirtium/README/master/1.svg?sanitize=true">

## Diagram of components/services

![image](https://user-images.githubusercontent.com/82182/91485584-fb7f6e80-e8a2-11ea-98ff-f1116f1bf2b4.png)
