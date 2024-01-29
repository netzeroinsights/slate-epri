---
title: Net Zero Insights API documentation for EPRI

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

# Startup Detail

All the information related to a startup is divided into different sections: 

1. [Overview and Taxonomy](#startup-overview-and-taxonomy)
2. [Patents](#startup-patents)
3. [Investors](#startup-investors)
4. [Contacts](#startup-contacts)
5. [Funding Rounds](#startup-funding-rounds)

Additionally, for each funding round, you can get the investors and the sources using the following endpoints:

1. [Investors](#funding-round-investors)
2. [Sources](#funding-round-sources)

## Startup Overview and Taxonomy

> To get a startup overview and taxonomy, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET "https://api.netzeroinsights.com/getStartup/sunfire-668"
```

> In case of a 200 response, the response body will contain the requested startup, with the format specified at section [Startup](#startup).

```json
{
  "clientID": 668,
  "name": "Sunfire",
  "logo": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1695114255/Startups/pwiujiclbklqjftnt16h.jpg",
  "website": "http://www.sunfire.de",
  "domain": "sunfire.de",
  "pitchLine": "Sunfire develops and manufactures industrial electrolysers for the production of renewable hydrogen and syngas.<br><br>The electrolyzers - based on alkaline and solid oxide technologies - are producing hydrogen and Syngas and are meant to decarbonize energy-intensive and climate-conscious businesses. The company either uses renewable electricity and water to produce green hydrogen, or includes captured CO2 in the process to produce renewable syngas which can be transferred into hydrocarbon products. Main applications for the produced fuels are refineries, steel manufacturing, chemicals, mobility, and the utility sector.<br><br>Sunfire develops an innovation that contributes to:<br>Climate change mitigation by producing green hydrogen and renewable syngas.<br>",
  "description": "Sunfire develops and produces high temperature electrolyzers SOEC and high temperature fuel cells SOFC Provider of energy conversion technologies including solid oxide fuel cells and renewable synthetic fuels based on solid oxide electrolyzers The solid oxide cells SOCs used for the conversion process are also used as generators to provide electricity and heat Sunfire has been named Global Cleantech 100 company for six consecutive years and is backed by leading strategic and financial investors such as Neste and SMS Group global leaders in the renewable fuel and steel business Innovative technology Sunfire offers modular power plants and electrolysis systems to produce renewable energy hydrogen and syngas Energy suppliers can work on a more efficient supply at certain points as the fuel cells can also use hydrocarbons Business ModelSunfire offers its technology in the fields of CHP off grid production and hydrogen fuels",
  "fundingAmount": 449000000,
  "fundingString": "449M",
  "fundingAmountUSD": 501968139,
  "fundingStringUSD": "502M",
  "fundingRangeID": 9,
  "fundingRange": ">250M",
  "lastRoundDate": "2023-08-31T06:52:00.000+00:00",
  "sustainabilityMetric": 0.9335,
  "foundedDate": 2010,
  "georowID": 814818,
  "countryID": 80,
  "country": "Germany",
  "city": "Dresden",
  "continent": "Europe",
  "email": "info@sunfire.de",
  "phone": "+49 351 8967970",
  "sizeID": 5,
  "size": "201 - 500",
  "stageID": 4,
  "stage": "Scaling",
  "linkedinURL": "https://www.linkedin.com/company/sunfire-gmbh/",
  "twitterURL": "https://twitter.com/sunfire_dresden/",
  "facebookURL": "https://facebook.com/sunfire.dresden/",
  "directURL": "sunfire-668",
  "sustainabilityMetricID": 4,
  "lastRoundAmount": 169000000,
  "lastRoundAmountUSD": 184431559,
  "lastRoundAmountString": "169M",
  "lastRoundAmountStringUSD": "184M",
  "lastRoundType": "Grant",
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
      "id": 374,
      "label": "climate change mitigation"
    },
    {
      "tagTypeId": 74,
      "tagType": {
        "tagType": "EU activity",
        "platformOrder": 9,
        "tagFamily": {
          "tagFamily": "EU taxonomy",
          "platformOrder": 1,
          "id": 1
        },
        "id": 74
      },
      "filterable": true,
      "id": 405,
      "label": "Manufacture of equipment for the production and use of hydrogen"
    }
  ],
  "trls": [
    {
      "date": "2023-12-06T12:36:34.167+00:00",
      "label": "6-8",
      "id": 4
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
  "roundCount": 11,
  "fundingRangeUSD": ">250M",
  "fundingRangeIDUSD": 9,
  "reviewDate": "2023-09-13T08:23:40.747+00:00",
  "lastReviewer": "pratibha_agarwal",
  "lastSeenDate": "2024-01-12T07:47:14.580+00:00",
  "numberOfEquityRounds": 8,
  "numberOfGrants": 3,
  "sustainabilityMetricLabel": "Very high impact",
  "employeesGrowthJSON": "[\n  {\n    \"dateOn\": {\n      \"month\": 12,\n      \"year\": 2021,\n      \"day\": 1\n    },\n    \"employeeCount\": 152\n  },\n  {\n    \"dateOn\": {\n      \"month\": 1,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 3,\n    \"employeeCount\": 157\n  },\n  {\n    \"dateOn\": {\n      \"month\": 2,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 1,\n    \"employeeCount\": 158\n  },\n  {\n    \"dateOn\": {\n      \"month\": 3,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 4,\n    \"employeeCount\": 164\n  },\n  {\n    \"dateOn\": {\n      \"month\": 4,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 2,\n    \"employeeCount\": 168\n  },\n  {\n    \"dateOn\": {\n      \"month\": 5,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 5,\n    \"employeeCount\": 177\n  },\n  {\n    \"dateOn\": {\n      \"month\": 6,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 5,\n    \"employeeCount\": 186\n  },\n  {\n    \"dateOn\": {\n      \"month\": 7,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 4,\n    \"employeeCount\": 194\n  },\n  {\n    \"dateOn\": {\n      \"month\": 8,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 5,\n    \"employeeCount\": 204\n  },\n  {\n    \"dateOn\": {\n      \"month\": 9,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 6,\n    \"employeeCount\": 216\n  },\n  {\n    \"dateOn\": {\n      \"month\": 10,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 11,\n    \"employeeCount\": 239\n  },\n  {\n    \"dateOn\": {\n      \"month\": 11,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 6,\n    \"employeeCount\": 253\n  },\n  {\n    \"dateOn\": {\n      \"month\": 12,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 3,\n    \"employeeCount\": 261\n  },\n  {\n    \"dateOn\": {\n      \"month\": 1,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 2,\n    \"employeeCount\": 266\n  },\n  {\n    \"dateOn\": {\n      \"month\": 2,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 3,\n    \"employeeCount\": 275\n  },\n  {\n    \"dateOn\": {\n      \"month\": 3,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 4,\n    \"employeeCount\": 285\n  },\n  {\n    \"dateOn\": {\n      \"month\": 4,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 1,\n    \"employeeCount\": 289\n  },\n  {\n    \"dateOn\": {\n      \"month\": 5,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 3,\n    \"employeeCount\": 298\n  },\n  {\n    \"dateOn\": {\n      \"month\": 6,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 4,\n    \"employeeCount\": 311\n  },\n  {\n    \"dateOn\": {\n      \"month\": 7,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 2,\n    \"employeeCount\": 318\n  },\n  {\n    \"dateOn\": {\n      \"month\": 8,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 2,\n    \"employeeCount\": 323\n  },\n  {\n    \"dateOn\": {\n      \"month\": 9,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 4,\n    \"employeeCount\": 336\n  },\n  {\n    \"dateOn\": {\n      \"month\": 10,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 5,\n    \"employeeCount\": 354\n  },\n  {\n    \"dateOn\": {\n      \"month\": 11,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 1,\n    \"employeeCount\": 359\n  },\n  {\n    \"dateOn\": {\n      \"month\": 12,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 0,\n    \"employeeCount\": 359\n  }\n]",
  "id": 527,
  "eutopiaScore": 93
}
```

To get a startup overview and taxonomy you should use the following endpoint:

`GET /getStartup/[directLink]`

It takes a single parameter, indicated as ”[directLink]” in the example, which is taken from a previous call of the endpoint at [Startup List](#startup-list), variable ”directLink”, and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Startup Patents

> To get a startup overview and taxonomy, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET "https://api.netzeroinsights.com/patents/668"
```

> In case of a 200 response, the response body will contain the requested patents, with the format specified at section [Patent](#patent).
     
```json
[
  {
    "id": 54136,
    "googlePatentsUrl": "https://patents.google.com/patent/DE112015006427A5/",
    "filingDate": "2015-04-07T22:00:00.000+00:00",
    "publicationDate": "2017-12-27T23:00:00.000+00:00",
    "patentAbstract": "A Process For The Production Of Synthetically Produced Methane (57)/Gaseous And/Or Liquid Hydrocarbons (114, 115, 116, 117). For This Purpose, Hydrogen (44, 84, 150) From An Electrolytic Arrangement (41, 81, 151, 159) Which Is Operated By Means Of Regeneratively Generated Electric Energy And Carbon Dioxide (19, 46, 86) Are Synthesized In A Methane Synthesis (Figs. 2-48) Or Fischer-Tropsch Synthesis (Figs. 3-96) Or Other Suitable Hydrocarbon Synthesis, The Carbon Dioxide (19, 46, 86) Being Produced From An Air/Gas Flow (3, 134) By Means Of A Carbon Dioxide Recovery System (Fig. 1). The Carbon Dioxide (19, 46, 86) Is Obtained From The Air/Gas Flow (3, 134) In The Carbon Dioxide Recovery System (Fig. 1) By Way Of A Reversible Adsorption Process. Also A Production System (57) For The Production Of Synthetically Produced Methane/Gaseous And/Or Liquid Hydrocarbons (114, 115, 116, 117), In Particular For Carrying Out The Production Process According To The Invention, Comprising An Electrolytic Arrangement (41, 81, 151, 159) Which Is Operated By Means Of Regeneratively Generated Electric Energy (42, 82, 153) For Producing Hydrogen (44, 84, 150), A Carbon Dioxide Recovery System (Fig. 1) For Producing Carbon Dioxide (19, 46, 86) From An Air/Gas Flow (3, 134) And A Methane (Fig. 2) Or Fischer-Tropsch Synthesis (Fig. 3) Or Any Other Suitable Hydrocarbon Synthesis For Synthesizing Hydrogen (44, 84, 150) And Carbon Dioxide (19, 45, 86) To Methane (57)/Gaseous And/Or Liquid Hydrocarbons (114, 115, 116, 117).",
    "title": "Production Process And Production System For Producing Methane / Gaseous And/Or Liquid Hydrocarbons",
    "jurisdiction": 80,
    "publicationNumber": "DE-112015006427-A5",
    "familyId": 1078,
    "clientId": 668,
    "jurisdictionName": "Germany",
    "status": "pending"
  },
  {
    "id": 54137,
    "googlePatentsUrl": "https://patents.google.com/patent/WO2016161998A1/",
    "filingDate": "2015-04-07T22:00:00.000+00:00",
    "publicationDate": "2016-10-12T22:00:00.000+00:00",
    "patentAbstract": "A Process For The Production Of Synthetically Produced Methane (57)/Gaseous And/Or Liquid Hydrocarbons (114, 115, 116, 117). For This Purpose, Hydrogen (44, 84, 150) From An Electrolytic Arrangement (41, 81, 151, 159) Which Is Operated By Means Of Regeneratively Generated Electric Energy And Carbon Dioxide (19, 46, 86) Are Synthesized In A Methane Synthesis (Figs. 2-48) Or Fischer-Tropsch Synthesis (Figs. 3-96) Or Other Suitable Hydrocarbon Synthesis, The Carbon Dioxide (19, 46, 86) Being Produced From An Air/Gas Flow (3, 134) By Means Of A Carbon Dioxide Recovery System (Fig. 1). The Carbon Dioxide (19, 46, 86) Is Obtained From The Air/Gas Flow (3, 134) In The Carbon Dioxide Recovery System (Fig. 1) By Way Of A Reversible Adsorption Process. Also A Production System (57) For The Production Of Synthetically Produced Methane/Gaseous And/Or Liquid Hydrocarbons (114, 115, 116, 117), In Particular For Carrying Out The Production Process According To The Invention, Comprising An Electrolytic Arrangement (41, 81, 151, 159) Which Is Operated By Means Of Regeneratively Generated Electric Energy (42, 82, 153) For Producing Hydrogen (44, 84, 150), A Carbon Dioxide Recovery System (Fig. 1) For Producing Carbon Dioxide (19, 46, 86) From An Air/Gas Flow (3, 134) And A Methane (Fig. 2) Or Fischer-Tropsch Synthesis (Fig. 3) Or Any Other Suitable Hydrocarbon Synthesis For Synthesizing Hydrogen (44, 84, 150) And Carbon Dioxide (19, 45, 86) To Methane (57)/Gaseous And/Or Liquid Hydrocarbons (114, 115, 116, 117).",
    "title": "Production Process And Production System For Producing Methane / Gaseous And/Or Liquid Hydrocarbons",
    "jurisdiction": 241,
    "publicationNumber": "WO-2016161998-A1",
    "familyId": 1078,
    "clientId": 668,
    "jurisdictionName": "World",
    "status": "pending"
  } 
]
```

To get all the patents of a startup, you should use the following endpoint:

`GET /patents/[clientID]`

It takes a single parameter, indicated as ”[clientID]” in the example, which is taken from a previous call of the endpoint at [Startup List](#startup-list), variable ”clientID”, and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Startup Investors

> To get all the investors of a startup, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET "https://api.netzeroinsights.com/investors/668"
```

> In case of a 200 response, the response body will contain the requested investors, with the format specified at section [Investor](#investor-core).

```json
[
  {
    "id": 13333,
    "name": "Amazon Climate Pledge Fund",
    "firstRoundDate": "Jul 2022",
    "roundTypes": "Late VC"
  },
  {
    "id": 19364,
    "name": "IPCEI",
    "firstRoundDate": "Jun 2022",
    "roundTypes": "Grant"
  }
]
```

To get all the investors of a startup, you should use the following endpoint:

`GET /investors/[clientID]`

It takes a single parameter, indicated as ”[clientID]” in the example, which is taken from a previous call of the endpoint at [Startup List](#startup-list), variable ”clientID”, and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Startup Contacts

> To get all the contacts of a startup, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X POST "https://api.netzeroinsights.com/contacts" \
-H "Content-Type: application/json" \
-d "{'clientID': 668, 'decisionMaker': false, 'roleID': 5}"
```

> In case of a 200 response, the response body will contain all the requested contacts, with the format specified at section [Contact](#contact).

```json
[
  {
    "name": "Hergen Wolf",
    "role": "Director Product Management",
    "department": "Tech",
    "email": "hergenthore.wolf@sunfire.de",
    "linkedinURL": "http://www.linkedin.com/in/hergen-wolf",
    "decisionMaker": true,
    "id": 1170662
  },
  {
    "name": "David Hering",
    "role": "Head Of Production",
    "department": "Tech",
    "email": "david.hering@sunfire.de",
    "linkedinURL": "http://www.linkedin.com/in/david-hering-07a169247",
    "decisionMaker": true,
    "id": 1170669
  }
]
```

To get all contacts of a startup, you should use the following endpoint:

`POST /contacts`

With a JSON request body in the format specified at the Section [Contacts Filter](#contacts-filter), and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Startup Funding rounds

> To get all the funding rounds of a startup, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET https://api.netzeroinsights.com/fundingRoundsPrints/668
```

> In case of a 200 response, the response body will contain the requested funding rounds, with the format specified at section [Funding Round](#funding-round).

```json
[
  {
    "clientId": 668,
    "roundDate": "2022-07-14T00:00:00.000+00:00",
    "roundType": "Late VC",
    "roundAmount": 0.0,
    "coFundingRoundId": 138720,
    "roundInvestors": [
      13333
    ],
    "roundNews": [
      58824,
      58825,
      58826
    ],
    "source": "pratik_gohil",
    "financingInstrument": "Equity",
    "equityStageID": 4,
    "exitStageID": 1,
    "id": 143791
  },
  {
    "clientId": 668,
    "roundDate": "2022-07-01T00:00:00.000+00:00",
    "roundType": "Grant",
    "roundAmount": 0.0,
    "coFundingRoundId": 177701,
    "roundInvestors": [
      19364
    ],
    "roundNews": [
      72998
    ],
    "source": "sharmila_bojan",
    "financingInstrument": "Grant",
    "equityStageID": 5,
    "exitStageID": 1,
    "id": 154414
  }
]
```

To get all the funding rounds of a startup, you should use the following endpoint:

`GET /fundingRoundsPrints/[clientID]`

It takes a single parameter, indicated as ”[clientID]” in the example, which is taken from a previous call of the endpoint at [Startup List](#startup-list), variable ”clientID”, and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Funding round investors

> To get all the investors of a given set of funding rounds, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X POST https://api.netzeroinsights.com/getFundingRoundInvestors \
-H "Content-Type: application/json" \
-d "{[86971]}"
```

> In case of a 200 response, the response body will contain all the investors of the requested funding rounds, with the format specified at section [Funding Round Investor](#funding-round-investor).

```json
[
  {
    "id": 10140,
    "name": "Blue Earth Capital",
    "website": "https://blueearth.capital/",
    "fundingRoundId": 86971
  },
  {
    "id": 3222,
    "name": "Carbon Direct Capital Management",
    "website": "https://carbon-direct.com/",
    "fundingRoundId": 86971
  },
  {
    "id": 6970,
    "name": "Copenhagen Infrastructure Partners",
    "website": "https://cipartners.dk/",
    "fundingRoundId": 86971
  }
]
```

To get all the investors of a given set of funding rounds, you should use the following endpoint:

`POST /getFundingRoundInvestors`

The request body should be a list of round IDs, which you can get from previous calls of [Startup Funding Rounds](#startup-funding-rounds), variable ”coFundingRoundId”, and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Funding round sources

> To get all the sources of a funding round, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
 -X GET https://api.netzeroinsights.com/roundNewsByRoundID/86971
```

> In case of a 200 response, the response body will contain all the sources of a funding rounds, with the format specified at section [Funding round source](#funding-round-source).

```json
[
  {
    "id": 50021,
    "url": "https://www.sunfire.de/en/news/detail/sunfire-secures-further-growth-capital-and-an-agreement-for-up-to-640-mw-electrolysis-offtake",
    "fundingRoundId": 86971
  },
  {
    "id": 39628,
    "url": "https://tech.eu/2022/03/24/sunfire-gets-eur195-million-backing-to-support-european-energy-independence",
    "fundingRoundId": 86971
  },
  {
    "id": 39629,
    "url": "https://renewablesnow.com/news/sunfire-raises-eur-86m-to-scale-electrolysers-production-778402/",
    "fundingRoundId": 86971
  }
]
```

To get all the sources of a funding round, you should use the following endpoint:

`GET /roundNewsByRoundID/[coFundingRoundId]`

It takes a single parameter, indicated as ”[coFundingRoundId]” in the example, which is taken from a previous call of the endpoint at Section [Startup Funding Rounds](#startup-funding-rounds), variable ”coFundingRoundId”, and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

# Investor Detail

> To get the details of an Investor, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET "https://api.netzeroinsights.com/getInvestor/10000"
```

> In case of a 200 response, the response body will contain the requested investor, with the format specified at section [Investor](#investor).

```json
{
  "investorID": 10000,
  "name": "Intergen",
  "description": "InterGen is a private ScaleUp fund and talent matching program based in Calgary, Canada.<br><br>The company was founded in 2018 with a belief that the talent and expertise responsible for making Alberta the economic envy of the entire continent for the last twenty years can be leveraged to build the companies that will define the next twenty years - and beyond. InterGen only invests in companies and CEOs that meet the criteria of having revenue of approximately $1M-$5M per year, with rare exceptions below $1M. The firm prefers to invest in seed-stage, early-stage, and later-stage companies in information technology, SaaS, TMT, oil, and gas sectors in Alberta. InterGen offers educational programming, events, and networking opportunities to help businesses learn as they grow. The company has a strong network of retired and transitioning executives looking to engage with innovative companies emerging from start-up to scale-up.",
  "website": "https://intergenconnect.com",
  "city": "Calgary",
  "country": "Canada",
  "continent": "North America",
  "linkedInURL": "https://www.linkedin.com/company/intergencanada/",
  "twitterURL": "https://twitter.com/intergenscaleup/",
  "email": "marcy@intergenconnect.com",
  "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1692058153/Investors/q3r0z1bzarioblbxnjmn.jpg",
  "size": "1 - 10",
  "sizeID": 1,
  "foundedDate": 2018,
  "numberOfDeals": 1,
  "numberOfDealsFiltered": 1,
  "lastDealType": "Late VC",
  "lastDealDate": "2018-12-14T00:00:00.000+00:00",
  "lastRoundAmount": 3294864,
  "lastRoundAmountUSD": 3750000,
  "note": "",
  "primaryTypeID": 10,
  "primaryType": "Venture Capital",
  "secondaryTypes": [],
  "investments": [
    {
      "id": 16936,
      "clientID": 31143,
      "url": "osperity-31143",
      "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1680109363/Startups/ihumccybullkimhjsinh.jpg",
      "name": "Osperity",
      "pitchline": "Osperity develops a cloud-based platform designed to offer intelligent visual monitoring services.<br><br>Osperity is a leading provider of AI-driven intelligent visual monitoring and alerting solutions for industrial operations. Their platform offers customizable exception-based management, remote site inspections, automated asset monitoring, and seamless integration with industrial sensors and systems, delivering business cost savings, risk mitigation, and operational efficiency.<br><br>Osperity develops an innovation that contributes to:<br>Climate change mitigation by providing a platform that offers visual monitoring services.",
      "country": "Canada",
      "totalFunding": 6283832,
      "totalFundingUSD": 7200000,
      "lastRoundType": "Late VC",
      "lastRoundAmount": 3294864,
      "lastRoundAmountUSD": 3750000,
      "lastRoundDate": "2018-12-14",
      "investorSince": "2018-12-14T00:00:00.000+00:00"
    }
  ],
  "coInvestors": [
    {
      "id": 16495,
      "investorID": 6998,
      "name": "Evok Innovations",
      "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1692355453/Investors/eek442rreqwc5qnaqtyw.jpg",
      "investorType": "Venture Capital",
      "country": "United States",
      "numberOfCoInvestments": 1
    },
    {
      "id": 5573,
      "investorID": 15357,
      "name": "Shell",
      "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1691834266/Investors/ov8ccgpalypyqaofecwl.jpg",
      "country": "United Kingdom",
      "numberOfCoInvestments": 1
    }
  ]
}
```

To get the investor information, you should use the following endpoint:

`GET /getInvestor/[investorID]`

It takes a single parameter, indicated as ”[investorID]” in the example, and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

# Deals List

> To get the deals list, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X POST 'https://api.netzeroinsights.com/getFundingRoundList' \
-H 'Content-Type: application/json' \                 
-d '{"limit": 1, "offset": 0, "include":{}, "exclude": {}, "fundingRoundInclude":{}, "fundingRoundExclude": {}, "investorInclude":{}, "investorExclude": {}, "sorting": {}}'
```

> In case of a 200 response, the response body will contain all the deals matching your request, with the format specified at section [Deals Search](#deals-search).

```json
{
  "roundsTotalFunding": 5.38828746078E11,
  "selectedCurrency": "USD",
  "count": 52018,
  "results": [
    {
      "clientId": 5051,
      "clientName": "Lightmatter",
      "clientLogoURL": "https://res.cloudinary.com/eutop-1/image/upload/b_white/v1685627341/Startups/rshobgpyjrff2mxdubu0.jpg",
      "clientPitchLine": "Lightmatter specializes in developing advanced computing solutions using an approach known as photonic computing. <br><br>Lightmatter provides photonic processors, utilizing light instead of electrons for faster and more energy-efficient computations. Their technology integrates optical components into existing semiconductor manufacturing processes, enabling faster data transfer rates while minimizing environmental impact. Lightmatter's photonic processors are designed for demanding applications such as AI, machine learning, and data analytics, providing faster training and inference times. <br><br>Lightmatter develops an innovation that contributes to:<br>Climate change mitigation by providing an energy-efficient alternative to traditional electronic processors.",
      "clientHQ": "United States",
      "clientCityHQ": "Boston",
      "clientCountryCode": "US",
      "clientCountryID": 226,
      "clientContinentID": 4,
      "clientFoundedDate": "2017",
      "roundDate": "2024-01-10T14:58:00.000+00:00",
      "roundType": "Series C",
      "roundAmount": 0.0,
      "roundInvestors": [
        10729
      ],
      "roundInvestorPOJOs": [
        {
          "id": 10729,
          "name": "Sip Global Partners",
          "website": "https://sipgp.com/",
          "fundingRoundId": 437610
        }
      ],
      "roundNewsPOJOs": [
        {
          "id": 127597,
          "title": "",
          "url": "https://www.finsmes.com/2024/01/lightmatter-receives-follow-on-investment-from-sip-global-partners-now-valued-at-1-2b.html",
          "coFundingRoundID": 437610
        },
        {
          "id": 99932,
          "title": "",
          "url": "",
          "coFundingRoundID": 437610
        }
      ],
      "numberOfRounds": 8,
      "totalFunding": 3.77524344E8,
      "totalFundingUSD": 4.22E8,
      "totalFundingString": "378M",
      "totalFundingStringUSD": "422M",
      "roundNumber": 6,
      "financingInstrument": "Equity",
      "lastRound": true,
      "equityStageID": 4,
      "exitStageID": 1,
      "id": 437610
    }
  ]
}
```

To search our deals database you should use the following endpoint:

`POST /getFundingRoundList`

With a JSON request body in the format specified at the section [Main Filter](#main-filter).

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

# Investors List

> To get the investors list, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X POST 'https://api.netzeroinsights.com/getInvestorList' \
-H 'Content-Type: application/json' \                 
-d '{"limit": 1, "offset": 0, "include":{}, "exclude": {}, "fundingRoundInclude":{}, "fundingRoundExclude": {}, "investorInclude":{}, "investorExclude": {}, "sorting": {}}'
```

> In case of a 200 response, the response body will contain all the investors matching your request, with the format specified at section [Investors Search](#investors-search).

```json
{
  "count": 22736,
  "totalFunding": 5.3894282550809375E11,
  "results": [
    {
      "investorID": 31522,
      "name": "Johannes Reck",
      "description": "Co-Founder & CEO at GetYourGuide.",
      "linkedInURL": "https://www.linkedin.com/in/johannesreck/",
      "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1703301964/Investors/kjaifkplzbgioerv6ufh.jpg",
      "numberOfDeals": 3,
      "numberOfDealsFiltered": 3,
      "lastDealType": "Pre-Seed",
      "lastDealDate": "2022-05-24T06:56:00.000+00:00",
      "note": "",
      "primaryTypeID": 44,
      "primaryType": "Angel",
      "secondaryTypes": [],
      "investments": [
        {
          "id": 103304,
          "clientID": 133823,
          "url": "tacto-133823",
          "logoURL": "https://res.cloudinary.com/eutop-1/image/upload/b_white/v1702653069/Startups/v7smvvz8vasm8fg1vfjy.jpg",
          "name": "Tacto",
          "pitchline": "Tacto helps mid-sized industrial organizations manage the rising complexity of supply chains.<br><br>Tacto's central operating system automates procurement workflows, ensuring compliance and sustainability in the supply chain. The software streamlines material sourcing and automates manual tasks related to regulatory compliance, including requirements from various Supply Chain Acts. It utilizes AI technology and advanced analytics to identify cost-saving opportunities in procurement spend by analyzing price developments in key cost drivers across the entire article portfolio.<br><br>Tacto develops an innovation that contributes to:<br>Climate change mitigation by enabling supply chain optimization.",
          "country": "Germany",
          "totalFunding": 55300000,
          "totalFundingUSD": 60433297,
          "lastRoundType": "Early VC",
          "lastRoundAmount": 50000000,
          "lastRoundAmountUSD": 54599708,
          "lastRoundDate": "2023-12-12",
          "investorSince": "2020-12-07T12:03:00.000+00:00"
        },
        {
          "id": 78453,
          "clientID": 102940,
          "url": "navit-102940",
          "logoURL": "https://res.cloudinary.com/eutop-1/image/upload/v1658420891/New_Empty_Logo_xqsrak.png",
          "name": "NAVIT",
          "pitchline": "NAVIT enables businesses to provide their employees with sustainable and flexible transportation options, accompanied by automated CO2 footprint calculations and offsetting.<br><br>NAVIT offers a platform that simplifies the management of employee mobility budgets through contemporary transportation options like car-sharing, bike subscriptions, and public transportation. By providing a monthly mobility budget, NAVIT eliminates the need for administrative tracking and allows employees to select their preferred mode of transportation, such as shared mobility, rented bikes or cars, or using fuel/charge cards for their personal vehicles. Additionally, the platform helps businesses measure, report, and offset their mobility-relevant carbon footprints.<br><br>NAVIT develops an innovation that contributes to:<br>Climate change mitigation by enabling carbon offsetting.<br>The transition to a circular economy by promoting shared mobility.",
          "country": "Germany",
          "totalFunding": 3500000,
          "totalFundingUSD": 3846066,
          "lastRoundType": "Seed",
          "lastRoundAmount": 3500000,
          "lastRoundAmountUSD": 3846066,
          "lastRoundDate": "2023-04-24",
          "investorSince": "2022-05-24T06:56:00.000+00:00"
        }
      ],
      "coInvestors": [
        {
          "id": 25583,
          "investorID": 31521,
          "name": "Torsten Reil",
          "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1703301895/Investors/oyjit8cen1fbmxaw31ag.jpg",
          "investorType": "Angel",
          "numberOfCoInvestments": 2
        },
        {
          "id": 390,
          "investorID": 2231,
          "name": "Visionaries Club",
          "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1691489048/Investors/v6p86exktszwvalmrtvm.jpg",
          "investorType": "Venture Capital",
          "country": "Germany",
          "numberOfCoInvestments": 2
        },
        {
          "id": 2781,
          "investorID": 9433,
          "name": "Michael Wax",
          "logoURL": "https://res.cloudinary.com/eutop-1/image/upload/v1658420891/New_Empty_Logo_xqsrak.png",
          "investorType": "Angel",
          "numberOfCoInvestments": 2
        },
        {
          "id": 2697,
          "investorID": 9194,
          "name": "Uvc Partners",
          "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1688443543/Investors/yavw0khx5vvqwz7zxvcv.jpg",
          "investorType": "Venture Capital",
          "country": "Germany",
          "numberOfCoInvestments": 2
        },
        {
          "id": 6557,
          "investorID": 17643,
          "name": "Hanno Renner",
          "logoURL": "https://res.cloudinary.com/eutop-1/image/upload/v1658420891/New_Empty_Logo_xqsrak.png",
          "investorType": "Angel",
          "country": "Germany",
          "numberOfCoInvestments": 2
        },
        {
          "id": 14220,
          "investorID": 664,
          "name": "Cherry Ventures",
          "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1691449060/Investors/lakn7t317zcr3aa3qnse.jpg",
          "investorType": "Private Equity",
          "country": "Germany",
          "numberOfCoInvestments": 1
        },
        {
          "id": 13112,
          "investorID": 26676,
          "name": "Arabella Capital",
          "logoURL": "https://res.cloudinary.com/eutop-1/image/upload/v1658420891/New_Empty_Logo_xqsrak.png",
          "numberOfCoInvestments": 1
        },
        {
          "id": 25989,
          "investorID": 31868,
          "name": "Christoph Bornschein",
          "logoURL": "https://res.cloudinary.com/eutop-1/image/upload/v1658420891/New_Empty_Logo_xqsrak.png",
          "investorType": "Angel",
          "numberOfCoInvestments": 1
        },
        {
          "id": 25990,
          "investorID": 31869,
          "name": "Javier Suarez",
          "logoURL": "https://res.cloudinary.com/eutop-1/image/upload/v1658420891/New_Empty_Logo_xqsrak.png",
          "investorType": "Angel",
          "numberOfCoInvestments": 1
        }
      ]
    }
  ]
}
```

To search our investors database you should use the following endpoint:

`POST /getInvestorList`

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

## Sorting

| Parameter name | Parameter type | Description                                                                 |
|----------------|----------------|-----------------------------------------------------------------------------|
| column         | string         | See Section [Sortable Columns](#sortable-columns) for the available options |
| direction      | string         | The only options available are ”ASC” and ”DESC”                             |

## Startups Filter

| Parameter name      | Parameter type                                      | Description                                                                       |
|---------------------|-----------------------------------------------------|-----------------------------------------------------------------------------------|
| searchableLocations | List of int                                         | See Section [Searchable Locations](#searchable-locations) for the accepted values |
| sizes               | List of Section [Size](#size)                       | Number of employees                                                               |
| stages              | List of int                                         | Growth stage, see Section [Stages](#stages) for accepted values                   |
| fundings            | List of int                                         | Total funding range, see Section [Fundings](#fundings) for accepted val- ues      |
| fundingsFrom        | int                                                 | Minimum total funding                                                             |
| fundingsTo          | int                                                 | Maximum total funding                                                             |
| tags                | List of int                                         | See Section [Tags](#tags) for accepted values                                     |
| trls                | List of int                                         | See Section [TRLs](#trls) for accepted values                                     |
| sustainabilities    | List of int                                         | See Section [Sustainabilities](#sustainabilities) for accepted values             |
| foundedDates        | List of Section [Founded Date](#founded-date)       | Startup founded date                                                              |
| acquisitionDateFrom | date                                                | Starting date for when the startup has been inserted into our database            |
| acquisitionDateTo   | date                                                | Maximum date for when the startup has been in- serted into our database           |
| foundedDatesFrom    | date                                                | Starting founded date                                                             |
| foundedDatesTo      | date                                                | Maximum founded date                                                              |
| raisedDateFrom      | date                                                | Starting date for any round                                                       |
| raisedDateTo        | date                                                | Maximum date for any round                                                        |
| lastRoundDates      | List of Section [Last Round Date](#last-round-date) | Date range for last round                                                         |
| lastRoundDatesFrom  | date                                                | Starting date for last round                                                      |
| lastRoundDatesTo    | date                                                | Maximum date for last round                                                       |
| numberOfRoundFrom   | int                                                 | Minimum number of rounds done by the company                                      |
| numberOfRoundTo     | int                                                 | Maximum number of rounds done by the company                                      |
| fundingTypes        | List of Section [Funding Type](#funding-type)       | Funding type for any round                                                        |
| sdgs                | List of int                                         | Sustainable development goals, see Section [SDGs](#sdgs) for accepted values      |
| wildcards           | List of string                                      | Any match of the keywords in the name/pitchline/description                       |
| wildcardsFields     | List of Section [Wildcard Fields](#wildcard-fields) | Select on which fields to match the wildcards                                     |
| investors           | List of int                                         | See Section [Investors](#investors) for the accepted values                       |
| lastFundingTypes    | List of Section [Funding Type](#funding-type)       | Funding type for last round                                                       |
| lastFundingsFrom    | List of int                                         | Minimum last round amount                                                         |
| lastFundingsTo      | List of int                                         | Maximum last round amount                                                         |
| patentSearch        | List of string                                      | Any match of the keywords in any patent description                               |
| patentsStatus       | List of Section [Patent Status](#patent-status)     | Status of any patent                                                              |
| applicationDateFrom | Date                                                | Starting application date for any patent                                          |
| applicationDateTo   | Date                                                | Maximum application date for any patent                                           |
| grantedDateFrom     | Date                                                | Starting granted date for any patent                                              |
| grantedDateTo       | Date                                                | Maximum granted date for any patent                                               |
| patentOffice        | List of int                                         | See Section [Searchable Locations](#searchable-locations) for the accepted values |
| patentsCountFrom    | int                                                 | Minimum number of patents                                                         |
| patentsCountTo      | int                                                 | Maximum number of patents                                                         |
| fundRaising         | List of string                                      | Use ”fundRaising” to see all the companies likely to fundraise                    |

## Deals Filter
 
| Parameter name       | Parameter type                              | Description                                                                                                     |                                                                                                    
|----------------------|---------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| dates                | List of RoundDate [Round Date](#round-date) | See Section [Round Date](#round-date) for the accepted values                                                   |                                                  
| acquisitionDateFrom  | Date                                        | Starting date for when the deal has been inserted into our database                                             |                                            
| acquisitionDateTo    | Date                                        | Maximum date for when the deal has been inserted into our database                                              |                                             
| datesFrom            | Date                                        | Starting date for when the deal has been closed                                                                 |                                                                
| datesTo              | Date                                        | Maximum date for when the deal has been closed                                                                  |                                                                 
| lastRoundDays        | List of int                                 | Maximun number of days passed since the deal was closed                                                         |
| amountFrom           | int                                         | Minimum deal amount                                                                                             |                                                                                            
| amountTo             | int                                         | Maximum deal amount                                                                                             |                                                                                            
| types                | List of int                                 | See Section [Deal Type](#deal-type) for the accepted values                                                     |                                                  
| allowNullAmounts     | boolean                                     | When searching with deal amount filters, if true, include deals with no deal amount                             |                            
| numberFrom           | int                                         | Minimum deal number for the company                                                                             |                                                                            
| numberTo             | int                                         | Maximum deal number for the company                                                                             |                                                                            
| investors            | List of int                                 | Using the [Investor List](#investors-list) endpoints, it is possible to fetch the investors' IDs to insert here |
| totalFundingFrom     | int                                         | Minimum total funding of the company                                                                            |                                                                           
| totalFundingTo       | int                                         | Maximum total funding of the company                                                                            |                                                                           
| financingInstruments | List of string                              | See Section [Financing Instruments](#financing-instrument) for the accepted values                              |                             
| equityStages         | List of int                                 | See Section [Equity Stage](#equity-stage) for the accepted values                                               |                                              
| exitStages           | List of int                                 | See Section [Exit Stage](#exit-stage) for the accepted values                                                   |                                                  

## Investors Filter

| Parameter name              | Parameter type | Description                                                                                                                  |
|-----------------------------|----------------|------------------------------------------------------------------------------------------------------------------------------|
| investorTypeIDs             | List of int    | See Section [Investor Types](#investor-types) for the accepted values                                                        |
| includeOtherInvestorTypes   | boolean        | When filtering for investor types, if true, include investors whose secondary types match at least one of the selected types |
| investorDealsFrom           | int            | Minimum number of deals                                                                                                      |
| investorDealsTo             | int            | Maximum number of deals                                                                                                      |
| investorSearchableLocations | List of int    | See Section [Searchable Locations](#searchable-locations) for the accepted values                                            |
| investorRegions             | List of int    | See Section [Investor Regions](#investor-regions) for accepted values                                                        |
| coInvestors                 | List of int    | See Section [Investors](#investors) for accepted values                                                                      |
| investments                 | List of int    | Using the endpoint [Startup List](#startup-list) it's possible to fetch their clientIDs to be used here                      |
| investorIDs                 | List of int    | See Section [Investors](#investors) for accepted values                                                                      |
| investorFoundedDatesFrom    | date           | Starting founded date of the investor                                                                                        |
| investorFoundedDatesTo      | date           | Maximum founded date of the investor                                                                                         |

## Contacts Filter

| Parameter name | Parameter type | Description                                                                                    |
|----------------|----------------|------------------------------------------------------------------------------------------------|
| clientID       | int            | ClientID of the requested startup, taken from a previous call of [Startup List](#startup-list) |
| decisionMaker  | boolean        | Optional, if true only returns contacts with decision making capabilities                      |
| roleID         | int            | Optional, contact role, see Section [Role](#role) for accepted values                          |

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

## Size

| ID | Label      |
|----|------------|
| 1  | 1-10       |
| 2  | 11-50      |
| 3  | 51-100     |
| 4  | 101-200    |
| 5  | 201-500    |
| 6  | 501-1000   |
| 7  | 1001-5000  |
| 8  | 5001-10000 |
| 9  | 10000+     |

## Founded Date

| ID | Label        |
|----|--------------|
| 1  | This year    |
| 2  | Last year    |
| 3  | Last 3 years |
| 4  | Last 5 years |

## Last Round Date

| ID | Label         |
|----|---------------|
| 1  | Last month    |
| 2  | Last semester |
| 3  | Last year     |

## Wildcard Fields

| Label          |
|----------------|
| pitchLine      |
| description    | 
| websiteContent |

## Patent Status

| Label   |
|---------|
| granted |
| pending |

## Stages

| ID | Label    |
|----|----------|
| 1  | Ideation |
| 2  | Early    |
| 3  | Growth   |
| 4  | Scaling  |

## TRLs

| ID | Label |
|----|-------|
| 2  | 9     |
| 3  | 1-5   |
| 4  | 6-8   |

## Fundings

| ID | Label       |
|----|-------------|
| 1  | 0 - 500K    |
| 2  | 500K - 1M   |
| 3  | 1M-5M       |
| 4  | 5M-10M      |
| 5  | 10M - 25M   |
| 6  | 25M - 50M   |
| 7  | 50M - 100M  |
| 8  | 100M - 250M |
| 9  | 250+M       |

## Sustainabilities

| ID | Label            |
|----|------------------|
| 1  | Low impact       |
| 2  | Average impact   |
| 3  | High impact      |
| 4  | Very high impact |

## Round Date

| ID | Label         |
|----|---------------|
| 1  | Last Month    |
| 2  | Last Quarter  |
| 3  | Last Semester |
| 4  | Last Year     |
| 5  | YTD           |

## SDGs

| ID | Label                                       |
|----|---------------------------------------------|
| 1  | 1. No poverty                               |
| 2  | 2. Zero hunger                              |
| 3  | 3. Good health and well-being               |
| 4  | 4. Quality education                        |
| 5  | 5. Gender equality                          |
| 6  | 6. Clean water and sanitation               |
| 7  | 7. Affordable and clean energy              |
| 8  | 8. Decent work and economic growth          |
| 9  | 9. Industry, innovation, and infrastructure |
| 10 | 10. Reduced inequalities                    |
| 11 | 11. Sustainable cities and communities      |
| 12 | 12. Responsible consumption and production  |
| 13 | 13. Climate action                          |
| 14 | 14. Life below water                        |
| 15 | 15. Life on land                            |
| 16 | 16. Peace justice and strong institutions   |
| 17 | 17. Partenrships                            |

## Financing Instrument

| Label  |
|--------|
| Debt   |
| Equity | 
| Grant  |

## Equity Stage

| ID | Label             |
|----|-------------------|
| 1  | Other             |
| 2  | Pre-seed and seed |
| 3  | Early stage       |
| 4  | Late stage        |

## Exit Stage

| ID | Label     |
|----|-----------|
| 1  | Venture   |
| 2  | Exit      |
| 3  | Post Exit |

## Deal Type

| ID  | Label                 |
|-----|-----------------------|
| 65  | Accelerator/incubator |
| 66  | Acquisition           |
| 70  | Convertible note      |
| 75  | Debt                  |
| 76  | Early VC              |
| 79  | Grant                 |
| 80  | Growth equity         |
| 81  | ICO                   |
| 82  | IPO                   |
| 83  | Late VC               |
| 84  | Merger                |
| 85  | PIPE                  |
| 88  | SPAC                  |
| 89  | Seed                  |
| 91  | Series A              |
| 92  | Series B              |
| 93  | Series C              |
| 94  | Series D              |
| 95  | Series E              |
| 96  | Series F              |
| 97  | Series G              |
| 98  | Series H              |
| 99  | Spinoff/spinout       |
| 102 | Pre-Seed              |
| 103 | Secondary transaction |
| 104 | Bridge                |
| 105 | In-kind services      |
| 107 | Award/Prize           |
| 108 | Private placement     |
| 109 | Product crowdfunding  |
| 110 | Equity crowdfunding   |
| 111 | Debt crowdfunding     |
| 112 | Revenue financing     |

## Role

| ID | Label          |
|----|----------------|
| 1  | Fouder         |
| 2  | HR             |
| 3  | Sales          |
| 4  | Marketing / PR |
| 5  | Tech           |
| 6  | C-Suite        |

## Investor Types

| ID | Label                     |
|----|---------------------------|
| 1  | Investment Bank           |
| 10 | Venture Capital           |
| 11 | Fund Of Funds             |
| 14 | Private Equity            |
| 17 | Hedge Fund                |
| 23 | Corporate Venture Capital |
| 24 | Angel Group               |
| 34 | Asset Manager             |
| 35 | Family Office             |
| 41 | Government                |
| 44 | Angel                     |
| 46 | Accelerator/Incubator     |
| 53 | University                |
| 57 | Real Estate               |
| 59 | Lender/Debt Provider      |
| 61 | Limited Partner           |
| 62 | Infrastructure            |
| 63 | Other                     |
| 64 | Corporation               |
| 68 | Commercial Banks          |
| 69 | Non-Profit Organisation   |
| 70 | Advisory Firm             |
| 71 | Wealth Management Firm    |
| 72 | Investment Company        |
| 73 | Insurance Company         |
| 74 | Sovereign Wealth Fund     |

## Investor Regions

| ID | Label                   |
|----|-------------------------|
| 1  | Alpine countries        |
| 2  | Balkan peninsula        |
| 3  | Baltics                 |
| 4  | Benelux                 |
| 5  | Central Europe          |
| 6  | Danubian countries      |
| 7  | Eastern Europe          |
| 8  | European Union          |
| 9  | Eurozone                |
| 10 | Iberian Peninsula       |
| 11 | Mediterranean countries |
| 12 | Nordics                 |
| 13 | Northern Europe         |
| 14 | Scandinavian peninsula  |
| 15 | Southern Europe         |
| 16 | Western Europe          |
| 17 | Europe                  |
| 19 | US Midwest              |
| 20 | US Northeast            |
| 21 | US Southeast            |
| 22 | US West                 |
| 23 | US East Coast           |
| 24 | US West Coast           |
| 25 | US Southwest            |

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

## Investors

> To get the list of the currently available investors, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET "https://api.netzeroinsights.com/getInvestorsForFilter"
```

> In case of a 200 response, the response body will contain all the available investors, with the JSON structured like the following:
     
```json
[
  {
    "id": 142,
    "name": "Hevella Capital",
    "website": "https://www.hevella-capital.com/"
  },
  {
    "id": 143,
    "name": "IBB Ventures",
    "website": "https://www.ibbventures.de/"
  }
]
```

To get the list of the currently available investors, you should use the following endpoint:

`GET /getInvestorsForFilter`

It takes no parameter, and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Funding Type

> To get the list of the currently available funding types, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET "https://api.netzeroinsights.com/getFundingTypes"
```

> In case of a 200 response, the response body will contain all the available funding types, with the JSON structured like the following:
     
```json
[
  {
    "name": "Accelerator/incubator",
    "id": 65
  },
  {
    "name": "Acquisition",
    "id": 66
  }
]
```

To get the list of the currently available funding types, you should use the following endpoint:

`GET /getFundingTypes`

It takes no parameter, and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Searchable Locations

> To get the list of the searchable locations, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET "https://api.netzeroinsights.com/searchLocation/london"
```

> In case of a 200 response, the response body will contain all the matching searchable locations, with the JSON structured like the following:
     
```json
[
  {
    "cityID": 112253,
    "cityName": "London",
    "adminID4": 3113,
    "adminName4": "England",
    "countryID": 225,
    "countryName": "United Kingdom",
    "continentID": 3,
    "continentName": "Europe",
    "id": 928071
  },
  {
    "cityID": 14534,
    "cityName": "London",
    "adminID4": 514,
    "adminName4": "Ontario",
    "countryID": 38,
    "countryName": "Canada",
    "continentID": 4,
    "continentName": "North America",
    "id": 775779
  }
]
```

To get the list of the searchable locations, you should use the following endpoint:

`GET /searchLocation/[location]`

It takes a single parameter, indicated as ”[location]” in the example, which is a string used to filter the locations and has the following response codes:

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

## Deal
        
| Name                   | Content                                                    |
|------------------------|------------------------------------------------------------|
| id                     | Internal funding round ID                                  |
| clientId               | Startup ID                                                 |
| clientName             | Startup name                                               |
| clientLogoURL          | URL to startup's logo                                      |
| clientPitchLine        | Startup pitchLine                                          |
| clientHQ               | Startup headquarters                                       |
| clientCityHQ           | Startup city's headquarters                                |
| clientCountryCode      | Startup country code                                       |
| clientCountryID        | Startup country ID                                         |
| clientContinentID      | Startup continent ID                                       |
| clientFoundedDate      | Startup founded date                                       |
| roundDate              | Date of the round                                          |
| acquisitionDate        | Date of startup insertion into our database                |
| roundType              | Type of the round                                          |
| roundAmount            | Amount of the round (EUR)                                  |
| roundAmountUSD         | Amount of the round (USD)                                  |
| roundAmountString      | Formatted amount of the round (EUR)                        |
| roundAmountStringUSD   | Formatted amount of the round (USD)                        |
| roundAmountRangeID     | Round amount range ID (EUR)                                |
| roundAmountRangeIDUSD  | Round amount range ID (USD)                                |
| roundInvestors         | List of IDs of all the investors of the round              |
| roundInvestorPOJOs     | List of IDs of all the investor DTOs of the round          |
| roundNews              | List of IDs of all the sources of the round                |
| roundNewsPOJOs         | List of IDs of all the source DTOs of the round            |
| roundCurrency          | Original currency of the round                             |
| originalRoundAmount    | Round amount in original currency                          |
| numberOfRounds         | Number of rounds of the company                            |        
| totalFundingRangeID    | Company total funding ID (EUR)                             |        
| totalFundingRangeIDUSD | Company total funding ID (USD)                             |        
| totalFunding           | Company total funding (EUR)                                |        
| totalFundingUSD        | Company total funding (USD)                                |        
| totalFundingString     | Formatted company total funding (EUR)                      |
| totalFundingStringUSD  | Formatted company total funding (USD)                      |
| roundNumber            | Number of the round for the company                        |
| financingInstrument    | Financing instrument                                       |
| lastRound              | If true, this is the latest round for the company          |
| source                 | Name of the analyst who inserted the round                 |
| valuationAmount        | Valuation amount                                           |
| valuationCurrency      | Valuation currency                                         |
| valuationType          | Valuation type                                             |
| equityStageID          | Equity stage ID, see Section [Equity Stage](#equity-stage) |
| exitStageID            | Exit stage ID, see Section [Exit Stage](#exit-stage)       |  
| insertionDate          | Date of insertion into our database                        |

## Deal search

| Name               | Content                                                      |
|--------------------|--------------------------------------------------------------|
| results            | List of Section [Deal](#deal)                                |
| count              | Total number of results, regardless of the ”limit” parameter |
| roundsTotalFunding | Total amount of results, regardless of the ”limit” parameter |
| selectedCurrency   | Selected currency of the user                                |    


## Funding round

| Name                | Content                                                    |
|---------------------|------------------------------------------------------------|
| id                  | Internal funding round ID                                  |
| clientID            | Startup ID                                                 |
| roundDate           | Date of the round                                          |
| roundType           | Type of the round                                          |
| roundAmount         | Amount of the round (EUR)                                  |
| roundAmountUSD      | Amount of the round (USD)                                  |
| roundAmountId       | ID of the amount range                                     |
| coFundingRoundId    | Additional internal funding round ID                       |
| fundingRange        | Amount range                                               |
| roundInvestors      | List of IDs of all the investors of the round              |
| roundNews           | List of IDs of all the sources of the round                |
| roundCurrency       | Original currency of the round                             |
| originalAmount      | Round amount in original currency                          |
| source              | Name of the analyst who inserted the round                 |
| financingInstrument | Financing instrument                                       |
| equityStageID       | Equity stage ID, see Section [Equity Stage](#equity-stage) |
| exitStageID         | Exit stage ID, see Section [Exit Stage](#exit-stage)       |

## Funding round investor

| Name           | Content              |
|----------------|----------------------|
| id             | Internal investor ID |
| name           | Investor name        |
| website        | Investor website     |
| fundingRoundId | Funding round ID     |

## Funding round source

| Name           | Content            |
|----------------|--------------------|
| id             | Internal source ID |
| url            | Source url         |
| fundingRoundId | Funding round ID   |

## Patent

| Name              | Content                                                    |
|-------------------|------------------------------------------------------------|
| id                | Internal patent ID                                         |
| googlePatentsUrl  | Patent url                                                 |
| filingDate        | Filing date                                                |
| publicationDate   | Pubblication date                                          |
| patentAbstract    | Patent abstract                                            |
| title             | Patent title                                               |
| jurisdiction      | Country ID where the patent has been filed                 |
| jurisdictionName  | Name of the country where the patent has been filed        |
| publicationNumber | External patent ID                                         |
| familyId          | Internal patent family ID                                  |
| clientId          | Client ID of the startup                                   |
| status            | Patent status, see Section [Patent Status](#patent-status) |

## Investor Core

| Name           | Content                                                                         |
|----------------|---------------------------------------------------------------------------------|
| id             | Internal investor ID                                                            |
| name           | Investor name                                                                   |
| firstRoundDate | Date of the first round of the company in which the investor made an appearance |
| roundTypes     | Types of round in which the investor appeared                                   |

## Contact

| Name          | Content                                             |
|---------------|-----------------------------------------------------|
| name          | Person name                                         |
| role          | Person role                                         |
| department    | Person department                                   |
| email         | Person email                                        |
| linkedinURL   | Person LinkedIn URL                                 |
| decisionMaker | True if the person has decision making capabilities |
| id            | Internal person ID                                  |

## Investor search

| Name         | Content                                                               |
|--------------|-----------------------------------------------------------------------|
| results      | List of Section [Investor](#investor)                                 |
| count        | Total number of results, regardless of the ”limit” parameter          |
| totalFunding | Total funding from the investors, regardless of the ”limit” parameter |

## Investor

| Name                  | Content                                                  |
|-----------------------|----------------------------------------------------------|
| id                    | Internal ID                                              |
| investorID            | Investor ID                                              |
| name                  | Name                                                     |
| description           | Description fetched from the investor website            |
| website               | Investor website                                         |
| city                  | City name                                                |
| country               | Country name                                             |
| continent             | Continent name                                           |
| linkedInURL           | URL to investor LinkedIn                                 |
| twitterURL            | URL to investor Twitter                                  |
| facebookURL           | URL to investor Facebook                                 |
| email                 | Investor main email                                      |
| phone                 | Investor main phone                                      |
| size                  | Investor number of employees range                       |
| sizeID                | Investor number of employees range ID                    |
| foundedDate           | Founded date                                             |
| numberOfDeals         | Number of deals                                          |
| numberOfDealsFiltered | Number of filtered deals                                 |
| lastDealType          | Type of the last deal                                    |
| lastDealDate          | Date of the last deal                                    |
| lastRoundAmount       | Last round amount in EUR                                 |
| lastRoundAmountUSD    | Last round amount in USD                                 |
| note                  | Note on the investor                                     |
| primaryTypeID         | Primary type ID                                          |
| primaryType           | Primary investor type                                    |
| secondaryTypes        | Secondary investor types                                 |
| investments           | List of companies that have been invested in             |
| coInvestors           | List of investors that have invested in mutual companies |

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

## Top Companies

> To get Top Companies of a Taxonomy Graph Item, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET 'https://api.netzeroinsights.com/taxonomy/graph/topCompanies/1783' \
-H 'Content-Type: application/json' \                 
```

> In case of a 200 response, the response body will contain at most 3 available companies of the specified item by ID, with the JSON structured like the following:

```json
[
    {
        "clientID": 112504,
        "name": "R3Energise",
        "logo": "https://res.cloudinary.com/eutop-1/image/upload/b_white/v1690205436/Startups/owsivo12opurbi23pgr7.jpg",
        "website": "https://www.r3energise.com/",
        "domain": "r3energise.com",
        "pitchLine": "R3Energise aims to support vessel operators in their transition to cleaner operations for their existing fleet. The ideal client grants R3Energise the opportunity to perform a feasibility study to assess the most suitable arrangement for their vessel, minimising the impact on their operations, CAPEX/OPEX and the environment. With our expertise ranging from CTV’s to ferries, survey vessels to SOV’s, R3Energise is a reliable partner in taking on these challenges and advising its clients.",
        "description": "",
        "fundingAmount": 124343.0,
        "fundingString": "124K",
        "fundingAmountUSD": 134097.0,
        "fundingStringUSD": "134K",
        "fundingRangeID": 1,
        "fundingRange": "0 - 500K",
        "lastRoundDate": "2023-01-01T13:31:00.000+00:00",
        "sustainabilityMetric": 0.2769792,
        "foundedDate": 2023,
        "georowID": 928883,
        "countryID": 225,
        "country": "United Kingdom",
        "city": "Colchester",
        "continent": "Europe",
        "email": "info@r3energise.com",
        "phone": "+44 7794 369903",
        "stageID": 1,
        "stage": "Ideation",
        "linkedinURL": "https://www.linkedin.com/company/r3energise-ltd/",
        "directURL": "r3energise-112504",
        "sustainabilityMetricID": 2,
        "lastRoundAmount": 124343,
        "lastRoundAmountUSD": 134097,
        "lastRoundAmountString": "124K",
        "lastRoundAmountStringUSD": "134K",
        "lastRoundType": "Grant",
        "tags": [
            {
                "tagTypeId": 4,
                "tagType": {
                    "tagType": "business model",
                    "platformOrder": 4,
                    "tagFamily": {
                        "tagFamily": "Business models",
                        "platformOrder": 4,
                        "id": 4
                    },
                    "id": 4
                },
                "filterable": true,
                "id": 303,
                "label": "service"
            }
        ],
        "fundingTypes": [],
        "sdgs": [
            {
                "id": 13,
                "label": "13. Climate action"
            }
        ],
        "note": "",
        "roundCount": 1,
        "fundingRangeUSD": "0 - 500K",
        "fundingRangeIDUSD": 1,
        "intellectualProperty": true,
        "numberOfGrants": 1,
        "sustainabilityMetricLabel": "Average impact",
        "id": 85443,
        "eutopiaScore": 27
    }
]
```

To get the top companies of a taxonomy item you should use the following endpoint:

`GET /taxonomy/graph/topCompanies/{itemID}`

Where the parameter `itemID` is the taxonomy item ID.

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Top Investors

> To get Top Investors of a Taxonomy Graph Item, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET 'https://api.netzeroinsights.com/taxonomy/graph/topInvestors/2' \
-H 'Content-Type: application/json' \                 
```

> In case of a 200 response, the response body will contain at most 3 available investors of the specified item by ID, with the JSON structured like the following:

```json
[
    {
        "investorID": 72,
        "name": "UK Research and Innovation",
        "logoURL": "https://res.cloudinary.com/eutop-1/image/upload/b_white/v1691668219/Investors/ocsr6c10pv9t7xumavd1.jpg",
        "numberOfDeals": 977,
        "numberOfDealsFiltered": 31,
        "id": 34
    },
    {
        "investorID": 670,
        "name": "Eit Innoenergy",
        "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1687594145/Investors/epm6ozsmb0awp9ljhvg3.jpg",
        "foundedDate": 2010,
        "numberOfDeals": 195,
        "numberOfDealsFiltered": 9,
        "primaryTypeID": 10,
        "primaryType": "Venture Capital",
        "id": 138
    },
    {
        "investorID": 18606,
        "name": "Sosv",
        "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1692150659/Investors/y4mrqtqfyeexi7yyo12r.jpg",
        "foundedDate": 1994,
        "numberOfDeals": 178,
        "numberOfDealsFiltered": 3,
        "primaryTypeID": 10,
        "primaryType": "Venture Capital",
        "id": 20830
    }
]
```

To get the top investors of a taxonomy item you should use the following endpoint:

`GET /taxonomy/graph/topInvestors/{itemID}`

Where the parameter `itemID` is the taxonomy item ID.

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
