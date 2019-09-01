<!--
GENERATED FILE - DO NOT EDIT
This file was generated by [MarkdownSnippets](https://github.com/SimonCropp/MarkdownSnippets).
Source File: /readme.source.md
To change this file edit the source file and then run MarkdownSnippets.
-->

# <img src="/src/icon.png" height="30px"> CountryData

[![Build status](https://ci.appveyor.com/api/projects/status/bb8461c5js69pn4x/branch/master?svg=true)](https://ci.appveyor.com/project/SimonCropp/australianelectorates) [![NuGet Status](https://img.shields.io/nuget/v/CountryData.svg?cacheSeconds=86400)](https://www.nuget.org/packages/CountryData/)

Provides a .net wrapper around the [GeoNames Data](https://www.geonames.org/). Also exposes the data as per country json files.

<!-- toc -->
## Contents

  * [NuGets](#nugets)
  * [Usage](#usage)
  * [Bogus Usage](#bogus-usage)
  * [Json Files](#json-files)
    * [Country Codes](#country-codes)
    * [Country Information](#country-information)
    * [Country Location Data](#country-location-data)
    * [Structure](#structure)
<!-- endtoc -->



## NuGets

The NuGets contain a static copy of all data. This data is embedded as resources inside the assembly. No network calls are done by the assembly. To get the latests version of the data do a NuGet update. There are several options to help keep a NuGet update:

 * [Dependabot](https://dependabot.com/): creates pull requests to keep your dependencies secure and up-to-date.
 * [Using NuGet wildcards](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#version-ranges-and-wildcards).
 * [Libraries.io](https://libraries.io/) supports subscribing to NuGet package updates.

https://nuget.org/packages/CountryData/

https://nuget.org/packages/CountryData.Bogus/


## Usage

<!-- snippet: usage -->
<a id='snippet-usage'/></a>
```cs
// All country info. This is only the country metadata
// and not all locationData.
var allCountryInfo = CountryLoader.CountryInfo;
var costaRicaInfo = allCountryInfo.Single(x => x.Iso == "CR");

// Loads all location data for a specific country
var australiaData = CountryLoader.LoadAustraliaLocationData();
var name = australiaData.Name;
var state = australiaData.States.First();
var province = state.Provinces.First();
var community = province.Communities.First();
var place = community.Places.First();
var postCode = place.PostCode;
var placeName = place.Name;
var latitude = place.Location.Latitude;
var longitude = place.Location.Longitude;
```
<sup>[snippet source](/src/Tests/Snippets.cs#L30-L49) / [anchor](#snippet-usage)</sup>
<!-- endsnippet -->


## Bogus Usage

<!-- snippet: bogususage -->
<a id='snippet-bogususage'/></a>
```cs
var faker = new Faker<Target>()
    .RuleFor(u => u.RandomCountryName, (f, u) => f.Country().Name())
    .RuleFor(u => u.RandomCountryCurrency, (f, u) => f.Country().CurrencyCode())
    .RuleFor(u => u.AustralianCapital, (f, u) => f.Country().Australia().Capital)
    .RuleFor(u => u.RandomIrelandState, (f, u) => f.Country().Ireland().State().Name)
    .RuleFor(u => u.RandomIcelandPostCode, (f, u) => f.Country().Iceland().PostCode());
var targetInstance = faker.Generate();
```
<sup>[snippet source](/src/Tests/Snippets.cs#L14-L24) / [anchor](#snippet-bogususage)</sup>
<!-- endsnippet -->


## Json Files


### Country Codes

List of country codes: https://raw.githubusercontent.com/SimonCropp/CountryData/master/Data/countrycodes.txt

```
https://raw.githubusercontent.com/SimonCropp/CountryData/master/Data/PostCodes/[CountryCode].json.txt
```


### Country Information

https://github.com/SimonCropp/CountryData/blob/master/Data/countryInfo.json.txt


### Country Location Data

For example the url for Australia (AU) is:

https://raw.githubusercontent.com/SimonCropp/CountryData/master/Data/PostCodes/AU.json.txt


### Structure

The GeoNames data is structured as:

Country > State > Province > Community > Place

However many countries do not have data for every level.


## Release Notes

See [closed milestones](../../milestones?state=closed).


## Icon

[World](https://thenounproject.com/term/world/956116/) designed by [Pedro Santos](https://thenounproject.com/pedrosantospt3) from [The Noun Project](https://thenounproject.com/pedrosantospt3).
