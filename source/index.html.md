---
title: Net Zero Insights API documentation

language_tabs:
  - shell

toc_footers:
  - <a href='https://netzeroinsights.com'>Visit our website</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: api documentation
    content: Documentation for the Net Zero Insights API
---

# Introduction

Our REST APIs give all the functionalities needed to interact with our database. All these services are exclusively usable with https standard, and only after having been authenticated.

For brevity, the possible error codes for all the calls are at the bottom of the document.

Every endpoint is to be called starting with the domain https://api.netzeroinsights.com

For testing purposes, we have a sandbox available at https://20.108.20.67

# Security

## Login

> To login, use this code:

```shell
curl -v -X POST "https://api.netzeroinsights.com/security/formLogin" \
-H "Content-Type: application/x-www-form-urlencoded" \
-d "username=YOUR_USERNAME&password=YOUR_PASSWORD"
```

> Make sure to replace `YOUR_USERNAME` and `YOUR_PASSWORD` with your credentials.
> 
> Using the -v ("verbose") flag lets you see the full response, in which you can find the **Session Cookie**.

Before using any other API, you should first login using the following endpoint:

`POST /security/formLogin`

With the following two parameters:

| Parameter name | Parameter value               |
|----------------|-------------------------------|
| username       | provided by Net Zero Insights |
| password       | provided by Net Zero Insights |

The possible response codes are:

| Response code | Meaning          |
|---------------|------------------|
| 200           | Login successful |

Please note that in case of a 200 response, you will also get a **Session Cookie**. You should save this,
as it will be needed for using all the other endpoints. The session cookie expires after 30 minutes of
session inactivity.

Our API expects the **Session Cookie** to be included in all API requests to the server, like this:

`JSESSIONID=EXAMPLE_SESSION_ID`

<aside class="notice">
You must replace <code>EXAMPLE_SESSION_ID</code> with your **Session Cookie**.
</aside>

## Logout

> To logout, use this code:

```shell
curl -v --cookie "JSESSIONID=EXAMPLE_SESSION_ID" \
 -X GET "https://api.netzeroinsights.com/security/logout"
```

> Make sure to replace `EXAMPLE_SESSION_ID` with your **Session Cookie**

To close the session, you should use the following endpoint:

`GET /security/logout`

It takes no parameter, and has the following response code:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Session terminated |

<aside class="notice">
Please note that manually closing a session is not required, since it will be closed bye the server after
30 minutes. This endpoint is mainly used if you need to use different accounts.
</aside>

# Startup List

> To get startup list, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X POST 'https://api.netzeroinsights.com/getStartupList' \
-H 'Content-Type: application/json' \                 
-d '{"limit": 1, "offset": 0, "include":{}, "exclude": {}, "fundingRoundInclude":{}, "fundingRoundExclude": {}, "investorInclude":{}, "investorExclude": {}, "sorting": {}}'
```

> In case of a 200 response, the response body will contain all the startups matching your request, with the format specified at section [Startup Search](#startup-search).

```json
{
  "count": 54856,
  "results": [
    {
      "clientID": 668,
      "name": "Sunfire",
      "logo": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1676009885/Startups/idgakaw4vpykudzpl978.jpg",
      "website": "http://www.sunfire.de",
      "domain": "sunfire.de",
      "pitchLine": "Sunfire develops and manufactures industrial electrolysers for the production of renewable hydrogen and syngas.<br><br>The electrolyzers - based on alkaline and solid oxide technologies - are producing hydrogen and Syngas and are meant to decarbonize energy-intensive and climate-conscious businesses. The company either uses renewable electricity and water to produce green hydrogen, or includes captured CO2 in the process to produce renewable syngas which can be transferred into hydrocarbon products. Main applications for the produced fuels are refineries, steel manufacturing, chemicals, mobility, and the utility sector.<br><br>Sunfire develops an innovation that contributes to:<br>Climate change mitigation by producing green hydrogen and renewable syngas.<br>",
      "description": "Developer of industrial electrolyzers designed to convert renewable electrical energy into fuels and gases. Innovative technology: Sunfire offers modular power plants and electrolysis systems to produce renewable energy, hydrogen and syngas. Provider of energy conversion technologies, including solid oxide fuel cells and renewable synthetic fuels based on solid oxide electrolyzers. Sunfire is an electrolysis company that designs and manufactures systems for the production of renewable industrial gas and fuel. A World Without Fossil Fuels. Sunfire develops and markets efficient energy supply concepts, which focus on the transformation of regenerative power into liquid petrol (power-to-liquids) or gas (power-to-gas). Develops and produces high-temperature fuel cells which facilitate the generation of electric power and heat. Developer of industrial electrolyzers designed to convert renewable electrical energy into fuels and gases. The company's renewable hydrogen and syngas as substitutes for fossil energy sources and offer electrolyzers based on alkaline and solid oxide (SOEC) technologies, enabling chemical, fuel, and steel industries to transform of energy Established in 2010 and based in Dresden, Germany, Sunfire is a world-leading industrial electrolysis company with two differentiated technologies. We develop and manufacture electrolyzers based on SOEC and Alkaline technologies that enable a truly sustainable and cost-effective production of renewable hydrogen, syngas and e-Fuel.\n\nSunfire has been named Global Cleantech 100 company for six consecutive years and is backed by leading strategic and financial investors such as Neste and SMS Group  global leaders in the renewable fuel and steel business. With more than 500 employees located in Germany and Switzerland and a well-established partner network, we realize large electrolysis projects to deliver on our promise: Creating a world without fossil fuels! Sunfire develops and manufactures systems for renewable industrial gas and fuel production. These substitutes for mineral oil and natural gas, known as e-Gas, e-Fuel or e-Chemicals, replace fossil fuels in existing infrastructures. The solid oxide cells (SOCs) used for the conversion process are also used as generators to provide electricity and heat.\n\nSunfires vision is to make regenerative energy from sources such as wind farms, hydropower plants, and photovoltaic systems available wherever and whenever it is needed  not just when the wind is blowing, the waves are crashing or the sun is shining. Established in 2010 and based in Dresden, Germany, Sunfire is a world-leading industrial electrolysis company with two differentiated technologies. We develop and manufacture electrolyzers based on SOEC and Alkaline technologies that enable a truly sustainable and cost-effective production of renewable hydrogen, syngas and e-Fuel.Sunfire has been named Global Cleantech 100 company for six consecutive years and is backed by leading strategic and financial investors such as Neste and SMS Group  global leaders in the renewable fuel and steel business. With more than 500 employees located in Germany and Switzerland and a well-established partner network, we realize large electrolysis projects to deliver on our promise: Creating a world without fossil fuels! ognised global leader for off-grid and CHP units based on solide oxide fuel cell technology. Renewables Everywhere. With the co-electrolysis of Sunfire, CO2-neutral synthetic crude oil can be produced from water in combination with carbon dioxide and green electricity via syngas. A breakthrough fuel cell and electrolyser technology replacingtheconventional fossil fuel used in your car with CO2 neutral fuel created from green power, water and CO2 fromtheatmosphere. CO2 & Hydrogen. Sunfire develops and manufactures systems for renewable industrial gas and fuel production. These substitutes for mineral oil and natural gas, known as e-Gas, e-Fuel or e-Chemicals, replace fossil fuels in existing infrastructures. The solid oxide cells (SOCs) used for the conversion process are also used as generators to provide electricity and heat. Sunfire develops and manufactures systems for renewable industrial gas and fuel production. These substitutes for mineral oil and natural gas, known as e-Gas, e-Fuel or e-Chemicals, replace fossil fuels in existing infrastructures. The solid oxide cells (SOCs) used for the conversion process are also used as generators to provide electricity and heat. Sunfires vision is to make regenerative energy from sources such as wind farms, hydropower plants, and photovoltaic systems available wherever and whenever it is needed  not just when the wind is blowing, the waves are crashing or the sun is shining. Sunfire develops and produces high temperature electrolyzers SOEC and high temperature fuel cells SOFC . As water vapour is used in electrolysis efficiencies of up to H methane and about for fuels are achieved.Customer ProblemTarget groups are energy chemical refinery and utility companies. Energy suppliers can work on a more efficient supply at certain points as the fuel cells can also use hydrocarbons.Business ModelSunfire offers its technology in the fields of CHP off grid production and hydrogen fuels. The product is then sold directly for individual orders.USPIn niche markets the special requirements and simpler logistics can give this system an economic advantage. Sunfire s entry markets are therefore small gas customers off grid applications and CHP plants for real estate.",
      "fundingAmount": 2.8E8,
      "fundingString": "280M",
      "fundingAmountUSD": 3.1753658E8,
      "fundingStringUSD": "318M",
      "fundingRangeID": 9,
      "fundingRange": ">250M",
      "lastRoundDate": "2022-07-14T00:00:00.000+00:00",
      "sustainabilityMetric": 0.9335,
      "foundedDate": 2010,
      "countryID": 80,
      "country": "Germany",
      "city": "Dresden",
      "continent": "Europe",
      "email": "info@sunfire.de",
      "phone": "+49 351 8967970",
      "sizeID": 2,
      "size": "11 - 50",
      "stageID": 4,
      "stage": "Scaling",
      "linkedinURL": "https://www.linkedin.com/company/sunfire-gmbh/",
      "twitterURL": "https://twitter.com/sunfire_dresden/",
      "facebookURL": "https://facebook.com/1382355191983196/",
      "directURL": "sunfire-668",
      "sustainabilityMetricID": 4,
      "lastRoundType": "Late VC",
      "tags": [
        {
          "tagTypeId": 74,
          "tagType": {
            "id": 74,
            "tagType": "EU activity",
            "platformOrder": 9,
            "tagFamily": {
              "id": 1,
              "tagFamily": "EU taxonomy",
              "platformOrder": 1
            }
          },
          "id": 405,
          "filterable": true,
          "label": "Manufacture of equipment for the production and use of hydrogen"
        },
        {
          "tagTypeId": 11,
          "tagType": {
            "id": 11,
            "tagType": "environmental objective",
            "platformOrder": 7,
            "tagFamily": {
              "id": 1,
              "tagFamily": "EU taxonomy",
              "platformOrder": 1
            }
          },
          "id": 374,
          "filterable": true,
          "label": "climate change mitigation"
        }
      ],
      "fundingTypes": [
        "Grant",
        "Equity"
      ],
      "sdgs": [
        {
          "id": 7,
          "label": "7. Affordable and clean energy"
        },
        {
          "id": 13,
          "label": "13. Climate action"
        }
      ],
      "note": "",
      "fundingRangeUSD": ">250M",
      "fundingRangeIDUSD": 9,
      "numberOfEquityRounds": 8,
      "numberOfGrants": 2,
      "id": 527,
      "eutopiaScore": 93
    }
  ]
}
```

To search our startup database you should use the following endpoint:

`POST /getStartupList`

With a JSON request body in the format specified at the section [Main Filter](#main-filter).

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |


# Filters structure

## Main Filter

This is the main filter used when searching for startups. It contains two simple fields (”offset” and ”limit”) and some complex ones (i.e.: ”include”, ”sorting”) defined further in this document.

| Parameter name      | Parameter type                                | Description                                                         |
|---------------------|-----------------------------------------------|---------------------------------------------------------------------|
| limit               | int                                           | Maximum number of results shown                                     |
| offset              | int                                           | Number of pages (of size "limit") skipped                           |
| sorting             | Section [Sorting](#sorting)                   | Order of the results                                                |
| include             | Section [Startups Filter](#startups-filter)   | Filters related to startups which should be included in the result  |
| exclude             | Section [Startups Filter](#startups-filter)   | Filters related to startups which should be excluded in the result  |
| fundingRoundInclude | Section [Deals Filter](#deals-filter)         | Filters related to deals which should be included in the result     |
| fundingRoundExclude | Section [Deals Filter](#deals-filter)         | Filters related to deals which should be excluded in the result     |
| investorInclude     | Section [Investors Filter](#investors-filter) | Filters related to investors which should be included in the result | 
| investorExclude     | Section [Investors Filter](#investors-filter) | Filters related to investors which should be excluded in the result |

# Additional Tables

## Sortable Columns

| Value                  | Usable for | Description                                 |
|------------------------|------------|---------------------------------------------|
| name                   | startup    | Startup name                                |
| country                | startup    | Startup country                             |
| website                | startup    | Startup website                             |
| foundedDate            | startup    | Startup founded date                        |
| size                   | startup    | Number of employees                         |
| stage                  | startup    | Startup growth stage                        |
| lastRoundDate          | startup    | Startup last round date                     |
| acquisitionDate        | startup    | Date of startup insertion into our database |
| fundingString          | startup    | Startup total funding                       |
| lastRoundAmount        | startup    | Startup last round amount                   |
| lastRoundType          | startup    | Startup last round type                     |
| sustainabilityMetricID | startup    | Startup impact on the ecosystem             |
| tags                   | startup    | Startup tags                                |
| fundingTypes           | startup    | Startup funding types                       |
| sdgs                   | startup    | Startup Sustainable Development Goals       |

## Tags

> To get the list of the currently available tags, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET "https://api.netzeroinsights.com/getEnabledTags"
```

> In case of a 200 response, the response body will contain all the available tags, with the JSON structured like the following:
     
```json
[
  {
    "name": "3d printing",
    "id": 1
  },
  {
    "name": "advanced material",
    "id": 2
  }
]
```

To get the list of the currently available tags, you should use the following endpoint:

`GET /getEnabledTags`

It takes no parameter, and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

# Responses structure

## Startup search

| Name    | Content                                                      |
|---------|--------------------------------------------------------------|
| results | List of Section [Startup](#startup)                          |
| count   | Total number of results, regardless of the ”limit” parameter |

## Startup

| Name                           | Content                                                  |
|--------------------------------|----------------------------------------------------------|
| id                             | Internal ID                                              |
| clientID                       | Startup ID                                               |
| name                           | Name                                                     |
| logo                           | URL to company’s logo                                    |
| website                        | Company website                                          |
| domain                         | Company website domain                                   |
| pitchLine                      | Pitchline                                                |
| description                    | Description fetched from the company website             |
| uniqueSellingProposition       | Unique selling proposition                               |
| impact                         | Company impact on climate                                |
| fundingAmount                  | Company total funding in EUR                             |
| fundingString                  | Company total funding in EUR, formatted                  |
| fundingAmountUSD               | Company total funding in USD                             |
| fundingStringUSD               | Company total funding in USD, formatted                  |
| fundingRange                   | Company total funding range                              |
| fundingRangeID                 | Company total funding range ID                           |
| fundingRangeUSD                | Company total funding range in USD                       |
| fundingRangeIDUSD              | Company total funding range ID in USD                    |
| lastRoundDate                  | Date of the last round                                   |
| acquisitionDate                | Date of insertion into our database                      |
| foundedDate                    | Founded date                                             |
| georowID                       | ID of the searchable location of the company HQ          |
| country                        | Country name                                             |
| countryID                      | Country ID                                               |
| city                           | City name                                                |
| cityID                         | City ID                                                  |
| continent                      | Continent name                                           |
| continentID                    | Continent ID                                             |
| admin1                         | Administrative region level 1 name                       |
| admin2                         | Administrative region level 2 name                       |
| admin3                         | Administrative region level 3 name                       |
| admin4                         | Administrative region level 4 name                       |
| admin1ID                       | Administrative region level 1 ID                         |
| admin2ID                       | Administrative region level 2 ID                         |
| admin3ID                       | Administrative region level 3 ID                         |
| admin4ID                       | Administrative region level 4 ID                         |
| email                          | Company main email                                       |
| phone                          | Company main phone                                       |
| size                           | Company number of employees range                        |
| sizeID                         | Company number of employees range ID                     |
| stage                          | Company growth stage                                     |
| stageID                        | Company growth stage ID                                  |
| employeesRange                 | Employees range                                          |
| linkedinURL                    | URL to company LinkedIn                                  |
| twitterURL                     | URL to company Twitter                                   |
| facebookURL                    | URL to company Facebook                                  |
| directURL                      | URL to our company page                                  |
| sustainabilityMetric           | Company climate impact metric score                      |
| sustainabilityMetricID         | Company climate impact metric range ID                   |
| sustainabilityMetricLabel      | Company climate impact metric label                      |
| lastRoundAmount                | Last round amount in EUR                                 |
| lastRoundAmountUSD             | Last round amount in USD                                 |
| lastRoundAmountString          | Last round amount in EUR, formatted                      |
| lastRoundAmountStringUSD       | Last round amount in USD, formatted                      |
| lastRoundType                  | Last round type                                          |
| revenueEuro                    | Total company revenue                                    |
| revenueYear                    | Year related to the ”revenueEuro” field                  |
| tags                           | Company tags                                             |
| trl                            | Company TRL                                              |
| trlID                          | Company TRL ID                                           |
| trlAcquisitionDate             | Last updated date of the company TRL                     |
| fundingTypes                   | Funding types of any round                               |
| sdgs                           | Sustainable Development Goals                            |
| investorPartnerSet             | Set of investorIDs                                       |
| companyContactSet              | Set of contact IDs                                       |
| isFundRaising                  | Company likelihood to fundraise                          |
| currentlyFundraising           | Estimation about the company being currently fundraising |
| currentlyFundraisingDate       | Date of estimation                                       |
| roundCount                     | Number of rounds                                         |
| roundWithDateCount             | Number of rounds with a date available                   |
| reviewDate                     | Date of latest company review by our analysts            |
| alternativeNames               | Alternative company names                                |
| legalNames                     | Legal company names                                      |
| intellectualProperty           | If true, the company has some registered IP              |
| pitchdeckURL                   | URL to the company pitch deck                            |
| lastPostMoneyValuation         | Latest post money valuation                              |
| lastPostMoneyValuationCurrency | Latest post money valuation currency                     |
| numberOfEquityRounds           | Number of company deals of type Equity                   |
| numberOfDebtRounds             | Number of company deals of type Debt                     |
| numberOfGrants                 | Number of company deals of type Grante                   |
| employeesGrowthJSON            | Historical aggregation of the employees fluctuation      |

> In case of a 200 response, the response body will contain the startup matching your request, with the format specified at section [Startup](#startup).

```json
{
  "clientID": 423,
  "name": "Kraftblock",
  "logo": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1692811618/Startups/a6oc6tki76sjozctvy78.jpg",
  "website": "http://www.kraftblock.com",
  "domain": "kraftblock.com",
  "pitchLine": "Kraftblock specializes in advanced thermal energy storage technology.<br><br>Kraftblock's core technology is multi-purpose, high-temperature energy storage that stores heat up to extreme temperatures in upcycled material. The systems either recycle waste heat or generate green heat via green power.<br><br>Kraftblock develops an innovation that contributes to:<br>Climate change mitigation by enabling industrial companies to replace fossil energy with renewable energy and recycle industrial waste heat.<br>The transition to a circular economy by using recycled material.",
  "description": "Kraftblock is the energy storage based on a bottom up materials development which enables the energy transition to 100 renewables in an ecological and economical sensfull way Kraftblock develops multifunctional energy storage solutions for heat and power that can enable the energy transition in industry with 30 and 60 MWh containers with efficient transformation also into electricity due to high storage temperature The company s systems store thermal energy from room temperature produced up to 85 from recycled materials and can store waste heat or converted power up to 1 300 C district heating or even repurposed conventional power plants which is preventive ecological fire retardant in ceilings floors fires from breaking out enabling customers to protect themselves during a fire outbreak and ensure safety It is universally applicable Power to Heat Heat to X and very cost effective thanks to the modular system",
  "fundingAmount": 23127686,
  "fundingString": "23.1M",
  "fundingAmountUSD": 25622914,
  "fundingStringUSD": "25.6M",
  "fundingRangeID": 5,
  "fundingRange": "10M - 25M",
  "lastRoundDate": "2023-08-08T14:47:00.000+00:00",
  "sustainabilityMetric": 0.9335,
  "foundedDate": 2014,
  "georowID": 817557,
  "countryID": 80,
  "country": "Germany",
  "city": "Saarbrücken",
  "continent": "Europe",
  "email": "welcome@kraftblock.com",
  "phone": "+49 6897 936161",
  "sizeID": 2,
  "size": "11 - 50",
  "stageID": 4,
  "stage": "Scaling",
  "linkedinURL": "https://www.linkedin.com/company/kraftblock/",
  "twitterURL": "https://twitter.com/kraftblocke/",
  "facebookURL": "https://facebook.com/kraftblock-575213782930847/",
  "directURL": "kraftblock-423",
  "sustainabilityMetricID": 4,
  "lastRoundAmount": 18327686,
  "lastRoundAmountUSD": 20000000,
  "lastRoundAmountString": "18.3M",
  "lastRoundAmountStringUSD": "20M",
  "lastRoundType": "Series B",
  "tags": [
    {
      "tagTypeId": 11,
      "tagType": {
        "tagType": "environmental objective",
        "platformOrder": 7,
        "tagFamily": {
          "tagFamily": "EU taxonomy",
          "platformOrder": 1,
          "id": 1
        },
        "id": 11
      },
      "filterable": true,
      "id": 377,
      "label": "the transition to a circular economy"
    },
    {
      "tagTypeId": 13,
      "tagType": {
        "tagType": "EU sector",
        "platformOrder": 9,
        "tagFamily": {
          "tagFamily": "EU taxonomy",
          "platformOrder": 1,
          "id": 1
        },
        "id": 13
      },
      "filterable": true,
      "id": 392,
      "label": "Manufacturing"
    }
  ],
  "trls": [
    {
      "date": "2023-08-14T17:01:30.977+00:00",
      "label": "9",
      "id": 2
    }
  ],
  "fundingTypes": [
    "Grant",
    "Equity"
  ],
  "sdgs": [
    {
      "id": 7,
      "label": "7. Affordable and clean energy"
    },
    {
      "id": 12,
      "label": "12. Responsible consumption and production"
    },
    {
      "id": 13,
      "label": "13. Climate action"
    }
  ],
  "note": "",
  "roundCount": 7,
  "fundingRangeUSD": "25M - 50M",
  "fundingRangeIDUSD": 6,
  "reviewDate": "2023-08-14T17:01:37.410+00:00",
  "lastReviewer": "amirhossein_mohammadghasemi",
  "lastSeenDate": "2024-01-12T08:38:17.433+00:00",
  "numberOfEquityRounds": 4,
  "numberOfGrants": 1,
  "sustainabilityMetricLabel": "Very high impact",
  "employeesGrowthJSON": "[\n  {\n    \"dateOn\": {\n      \"month\": 12,\n      \"year\": 2021,\n      \"day\": 1\n    },\n    \"employeeCount\": 19\n  },\n  {\n    \"dateOn\": {\n      \"month\": 1,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 11,\n    \"employeeCount\": 21\n  },\n  {\n    \"dateOn\": {\n      \"month\": 2,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 5,\n    \"employeeCount\": 22\n  },\n  {\n    \"dateOn\": {\n      \"month\": 3,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 5,\n    \"employeeCount\": 23\n  },\n  {\n    \"dateOn\": {\n      \"month\": 4,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 0,\n    \"employeeCount\": 23\n  },\n  {\n    \"dateOn\": {\n      \"month\": 5,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 4,\n    \"employeeCount\": 24\n  },\n  {\n    \"dateOn\": {\n      \"month\": 6,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 0,\n    \"employeeCount\": 24\n  },\n  {\n    \"dateOn\": {\n      \"month\": 7,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 4,\n    \"employeeCount\": 25\n  },\n  {\n    \"dateOn\": {\n      \"month\": 8,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 4,\n    \"employeeCount\": 26\n  },\n  {\n    \"dateOn\": {\n      \"month\": 9,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": -4,\n    \"employeeCount\": 25\n  },\n  {\n    \"dateOn\": {\n      \"month\": 10,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 4,\n    \"employeeCount\": 26\n  },\n  {\n    \"dateOn\": {\n      \"month\": 11,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 4,\n    \"employeeCount\": 27\n  },\n  {\n    \"dateOn\": {\n      \"month\": 12,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 0,\n    \"employeeCount\": 27\n  },\n  {\n    \"dateOn\": {\n      \"month\": 1,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 0,\n    \"employeeCount\": 27\n  },\n  {\n    \"dateOn\": {\n      \"month\": 2,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 0,\n    \"employeeCount\": 27\n  },\n  {\n    \"dateOn\": {\n      \"month\": 3,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": -4,\n    \"employeeCount\": 26\n  },\n  {\n    \"dateOn\": {\n      \"month\": 4,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": -4,\n    \"employeeCount\": 25\n  },\n  {\n    \"dateOn\": {\n      \"month\": 5,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": -4,\n    \"employeeCount\": 24\n  },\n  {\n    \"dateOn\": {\n      \"month\": 6,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 0,\n    \"employeeCount\": 24\n  },\n  {\n    \"dateOn\": {\n      \"month\": 7,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": -4,\n    \"employeeCount\": 23\n  },\n  {\n    \"dateOn\": {\n      \"month\": 8,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 0,\n    \"employeeCount\": 23\n  },\n  {\n    \"dateOn\": {\n      \"month\": 9,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 13,\n    \"employeeCount\": 26\n  },\n  {\n    \"dateOn\": {\n      \"month\": 10,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 12,\n    \"employeeCount\": 29\n  },\n  {\n    \"dateOn\": {\n      \"month\": 11,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 3,\n    \"employeeCount\": 30\n  },\n  {\n    \"dateOn\": {\n      \"month\": 12,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 0,\n    \"employeeCount\": 30\n  }\n]",
  "id": 20186,
  "eutopiaScore": 93
}
```

# Taxonomy Page

Our taxonomy is a way to visualise the relation between different topics.

## All Taxonomy Items

> To get all Taxonomy Graph Items, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET 'https://api.netzeroinsights.com/taxonomy/itemDtos' \
-H 'Content-Type: application/json' \                 
```

> In case of a 200 response, the response body will contain all the available items, with the JSON structured like the following:

```json
[
  {
    "label": "Alternative Fuel",
    "description": "Alternative fuels are at the forefront of innovation, with notable examples being biofuels and synthetic fuels. Solutions in this domain are dedicated to advancing and applying these alternatives, not only for transportation but also for broader energy applications, including electricity generation and industrial processes.",
    "tagID": 995,
    "tagName": "Alternative Fuel",
    "rawSuggestedSearches": [
      "{\"include\": {\"tags\": [323], \"wildcardsFields\": [\"pitchLine\"]}, \"exclude\": {\"tags\": [212, 220, 224]}}"
    ],
    "id": 1
  },
  {
    "label": "Biofuel",
    "description": "Biofuels are produced from renewable resources, primarily plant-based feedstocks such as crops, agricultural residues, or algae. Biofuels offer a way to decarbonize sectors that are challenging to electrify, such as aviation and heavy industry, while promoting agricultural sustainability through responsible feedstock sourcing and land-use practices. Some solutions include innovative processes to convert biomass into biofuels, such as biodiesel and bioethanol, through techniques like fermentation and thermochemical conversion.",
    "tagID": 996,
    "tagName": "Biofuel",
    "rawSuggestedSearches": [
      "{\"include\":{\"tags\":[20,374]},\"exclude\":{},\"fundingRoundInclude\":{},\"fundingRoundExclude\":{},\"investorInclude\":{},\"investorExclude\":{}}",
      "{\"include\":{\"wildcardsFields\":[\"pitchLine\"],\"regexpFields\":[\"pitchLine\"],\"regexps\":[\"produc[a-z]{0,5}[^A-z0-9]+([A-z0-9]+[^A-z0-9]+){0,5}biofuel[a-z]{0,5}\"]},\"exclude\":{},\"fundingRoundInclude\":{},\"fundingRoundExclude\":{},\"investorInclude\":{},\"investorExclude\":{}}",
      "{\"include\":{\"wildcardsFields\":[\"pitchLine\"],\"regexpFields\":[\"pitchLine\"],\"regexps\":[\"manufactur[a-z]{0,5}[^A-z0-9]+([A-z0-9]+[^A-z0-9]+){0,5}biofuel[a-z]{0,5}\"]},\"exclude\":{},\"fundingRoundInclude\":{},\"fundingRoundExclude\":{},\"investorInclude\":{},\"investorExclude\":{}}",
      "{\"include\":{\"wildcardsFields\":[\"pitchLine\"],\"regexpFields\":[\"pitchLine\",\"description\"],\"regexps\":[\"offer[a-z]{0,5}[^A-z0-9]+([A-z0-9]+[^A-z0-9]+){0,5}biofuel[a-z]{0,5}\"]},\"exclude\":{},\"fundingRoundInclude\":{},\"fundingRoundExclude\":{},\"investorInclude\":{},\"investorExclude\":{}}",
      "{\"include\":{\"tags\":[20],\"wildcards\":[\"biofuel\"],\"wildcardsFields\":[\"pitchLine\"],\"regexpFields\":[\"pitchLine\"]},\"exclude\":{},\"fundingRoundInclude\":{},\"fundingRoundExclude\":{},\"investorInclude\":{},\"investorExclude\":{}}",
      "{\"include\":{\"wildcardsFields\":[\"pitchLine\"],\"regexpFields\":[\"pitchLine\",\"description\"],\"regexps\":[\"develop[a-z]{0,5}[^A-z0-9]+([A-z0-9]+[^A-z0-9]+){0,5}biofuel[a-z]{0,5}\"]},\"exclude\":{},\"fundingRoundInclude\":{},\"fundingRoundExclude\":{},\"investorInclude\":{},\"investorExclude\":{}}"
    ],
    "id": 2
  }
]
```

To get all the taxonomy items you should use the following endpoint:

`GET /taxonomy/itemDtos`

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Level 0 Taxonomy Graph Items

> To get Taxonomy Graph Item list without any parents (which means they are the top level of our taxonomy), use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET 'https://api.netzeroinsights.com/taxonomy/graph' \
-H 'Content-Type: application/json' \                 
```

> In case of a 200 response, the response body will contain all the available taxonomy graph items, with the JSON structured like the following:

```json
[
  {
    "label": "Solutions map",
    "description": "The Solutions Map simplifies your exploration of climate tech solutions. We've categorized over 200 solutions into Challenge Areas like Energy, Industry, Transport, and more. When you choose a solution, you can dive into its sub-solutions if they exist. You can also access insights, active investors, and information about startups and SMEs for each solution.",
    "tagID": 1399,
    "companyCount": 39491,
    "dealCount": 41425,
    "totalFunding": 424336443804,
    "totalFundingUSD": 473836670179,
    "hasChildren": true,
    "id": 347
  },
  {
    "label": "Deep Dives map",
    "description": "The Deep Dives offers a meticulous mapping of the most innovative and extensively researched fields in the realm of Climate Tech. These curated maps serve as a direct, technologically advanced interface, simplifying navigation through the intricate landscape of climate technology. Users can seamlessly delve into specific areas such as Cement and Concrete, Carbon Offset and Markets, Marine Energy, and Hydrogen, gaining valuable insights into advancements, sub-solutions, and active investors. ",
    "tagID": 1412,
    "companyCount": 68748,
    "dealCount": 0,
    "totalFunding": -9223372036854775808,
    "totalFundingUSD": -9223372036854775808,
    "hasChildren": true,
    "id": 359
  },
  {
    "label": "Software map",
    "description": "The Software Map is a comprehensive visual representation that outlines the diverse array of software solutions within the climate tech landscape. This map provides a detailed overview of software applications tailored to address climate challenges across various sectors, including energy, transport, industry, food and agriculture, built environment, natural environment, and more. ",
    "tagID": 1823,
    "companyCount": 68850,
    "dealCount": 0,
    "totalFunding": -9223372036854775808,
    "totalFundingUSD": -9223372036854775808,
    "hasChildren": true,
    "id": 660
  }
]
```

To get all the level 0 taxonomy items you should use the following endpoint:

`GET /taxonomy/graph`

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

These are the top-most items of our taxonomy, and all the other items are related to them, either directly or through another item(s)

## Taxonomy Graph children Items

> To get the list of children Taxonomy Graph Items of a parent item, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET 'https://api.netzeroinsights.com/taxonomy/graph/Biofuel' \
-H 'Content-Type: application/json' \                 
```
> Or

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET 'https://api.netzeroinsights.com/taxonomy/graph/2' \
-H 'Content-Type: application/json' \                 
```

> In case of a 200 response, the response body will contain all the available children items of a parent item by ID or label, with the JSON structured like the following:
 
```json
[
  {
    "label": "Bioethanol",
    "description": "Bioethanol is produced through the fermentation of organic materials, such as crops like corn, and sugarcane, or cellulose-rich feedstocks like switchgrass. This process converts the sugars within these materials into ethanol using microorganisms. Bioethanol is a key player in the quest for sustainable transportation fuels, as it can be blended with gasoline to reduce greenhouse gas emissions and dependence on fossil fuels. When compared to other sustainable fuels like biodiesel or synthetic fuels, bioethanol has specific advantages, such as its compatibility with existing gasoline engines and infrastructure.",
    "tagID": 1093,
    "companyCount": 0,
    "dealCount": 0,
    "hasChildren": false,
    "id": 5
  },
  {
    "label": "Bio-Oil",
    "description": "Bio-oil is produced from biomass sources like wood chips, agricultural residues, or algae. It is typically created through a process called pyrolysis or fast pyrolysis, which involves heating biomass in the absence of oxygen to break it down into a liquid form. Bio-oil can be used as a replacement for traditional fossil fuels in applications such as power generation and heating, and it can also serve as a feedstock for the production of biofuels and other valuable chemicals. Compared to other sustainable fuels like bioethanol or biodiesel, bio-oil offers advantages such as a higher energy density and the potential for versatile applications.",
    "tagID": 1094,
    "companyCount": 27,
    "dealCount": 14,
    "totalFunding": 1924706,
    "totalFundingUSD": 2264121,
    "hasChildren": false,
    "id": 6
  }
]
```

To get all the children taxonomy items of a parent item, you should use the following endpoint:

`GET /taxonomy/graph/{parentID}`

Where the parameter `parentID` can either be the parent item ID or the parent item label.

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Taxonomy Item

> To get a Taxonomy Graph Item by parameter, ID or label, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET 'https://api.netzeroinsights.com/taxonomy/item/2' \
-H 'Content-Type: application/json' \                 
```

> Or

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET 'https://api.netzeroinsights.com/taxonomy/item/Biofuel' \
-H 'Content-Type: application/json' \                 
```

> In case of a 200 response, the response body will contain a taxonomy graph item, with the JSON structured like the following:

```json
{
    "label": "Biofuel",
    "description": "Biofuels are produced from renewable resources, primarily plant-based feedstocks such as crops, agricultural residues, or algae. Biofuels offer a way to decarbonize sectors that are challenging to electrify, such as aviation and heavy industry, while promoting agricultural sustainability through responsible feedstock sourcing and land-use practices. Some solutions include innovative processes to convert biomass into biofuels, such as biodiesel and bioethanol, through techniques like fermentation and thermochemical conversion.",
    "tagID": 1090,
    "companyCount": 70,
    "dealCount": 62,
    "totalFunding": 1188638956,
    "totalFundingUSD": 222394728,
    "hasChildren": true,
    "id": 2
}
```

To get a single taxonomy item you should use the following endpoint:

`GET /taxonomy/item/{itemID}`

Where the parameter `itemID` can either be the item ID or the item label.

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Taxonomy Item Relations by ParentID

> To get Taxonomy Graph Item Relation list by parentID, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET 'https://api.netzeroinsights.com/taxonomy/relations/parent/1' \
-H 'Content-Type: application/json' \                 
```

> In case of a 200 response, the response body will contain all the available taxonomy graph item relations, with the JSON structured like the following:

```json
[
  {
    "id": 0,
    "parentID": 1,
    "childID": 3,
    "parentLabel": "Alternative Fuell",
    "childLabel": "Electrofuels"
  },
  {
    "id": 1,
    "parentID": 1,
    "childID": 4,
    "parentLabel": "Alternative Fuell",
    "childLabel": "Synthetic Fuel"
  }
]
```

To get all the parent-children relations of a taxonomy item you should use the following endpoint:

`GET /relations/parent/{itemID}`

Where the parameter `itemID` is the taxonomy item ID.

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Taxonomy Item Relations by ChildID

> To get Taxonomy Graph Item Relation list by childID, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET 'https://api.netzeroinsights.com/taxonomy/relations/child/24' \
-H 'Content-Type: application/json' \                 
```

> In case of a 200 response, the response body will contain all the available taxonomy graph item relations, with the JSON structured like the following:

```json
[
  {
    "id": 0,
    "parentID": 22,
    "childID": 24,
    "parentLabel": "Solar Energy",
    "childLabel": "Photovoltaic"
  }
]
```

To get all the child-parents relations of a taxonomy item you should use the following endpoint:

`GET /relations/child/{itemID}`

Where the parameter `itemID` is the taxonomy item ID.

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |
