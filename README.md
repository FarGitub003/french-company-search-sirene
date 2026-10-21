# French Company Search – SIREN, SIRET & NAF (Sirene)

Search French companies by name, SIREN, SIRET, NAF code, department or legal form in the open Sirene data. Legal entities only: no directors, no sole traders. Licence attribution in every record, optional new-or-changed mode.

**▶ Run it on Apify Store: https://apify.com/far003/french-company-search-sirene**

> This repository hosts documentation and examples; the Actor runs on the Apify platform.

## What it does

- Looks up French companies by name, SIREN, SIRET, NAF (APE) activity code, department, postal code, legal form and size, and returns clean, flat JSON records.
- Legal entities only: no directors, shareholders or sole traders are requested or delivered.
- The licence attribution (`source`, `sourceLicense`, `sourceUpdatedAt`, `retrievedAt`) is in every record.
- Optional "new or changed only" mode (`onlyNewOrChanged`) that lists the fields that changed.

## Who it is for

- KYB and onboarding checks.
- CRM enrichment and deduplication.
- Market mapping and lead lists.
- Monitoring a segment of companies over time.

## Example input

```json
{
  "queries": ["DANONE", "552032534"],
  "departments": ["75"],
  "nafCodes": ["62.01Z"],
  "status": "active",
  "maxResultsPerQuery": 100
}
```

## Example output

<details><summary>Show the record</summary>

```json
{
  "status": "active",
  "query": "552 032 534",
  "queriedSiret": null,
  "establishmentStatus": null,
  "establishmentClosedDate": null,
  "requestedEstablishment": null,
  "siren": "552032534",
  "siret": "55203253400703",
  "name": "DANONE",
  "legalName": "DANONE",
  "acronym": null,
  "legalFormCode": "5599",
  "legalFormLabel": "SA à conseil d'administration (s.a.i.)",
  "nafCode": "70.10Z",
  "nafCodeNaf25": "70.10Y",
  "nafSection": "M",
  "companyCategory": "GE",
  "employeeRangeCode": "42",
  "employeeRangeLabel": "1 000 à 1 999 salariés",
  "employeeRangeYear": 2024,
  "headOfficeIsEmployer": true,
  "creationDate": "1955-01-01",
  "closureDate": null,
  "establishmentCount": 19,
  "openEstablishmentCount": 3,
  "address": "59-61 RUE LA FAYETTE 75009 PARIS",
  "postalCode": "75009",
  "city": "PARIS",
  "cityCode": "75109",
  "department": "75",
  "region": "11",
  "latitude": 48.8763540066087,
  "longitude": 2.34353640229216,
  "headOfficeCreationDate": "2025-08-19",
  "headOfficeStatus": "active",
  "headOfficeInArea": null,
  "matchedEstablishments": null,
  "sourceUpdatedAt": "2026-09-10T13:14:57",
  "change": null,
  "changedFields": null,
  "duplicateOf": null,
  "note": null,
  "source": "INSEE – base Sirene (www.insee.fr), retrieved through the API Recherche d'entreprises (DINUM)",
  "sourceLicense": "Licence Ouverte 2.0 / Open Licence 2.0 (Etalab)",
  "retrievedAt": "2026-10-13T13:12:00.000Z"
}
```

</details>

## Use it from code

Set your token in the `APIFY_TOKEN` environment variable.

**Node.js** ([`apify-client`](https://docs.apify.com/api/client/js/))

```js
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('far003/french-company-search-sirene').call({
    "queries": [
        "DANONE",
        "552032534"
    ],
    "departments": [
        "75"
    ],
    "nafCodes": [
        "62.01Z"
    ],
    "status": "active",
    "maxResultsPerQuery": 100
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

**Python** ([`apify-client`](https://docs.apify.com/api/client/python/))

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("far003/french-company-search-sirene").call(run_input={
    "queries": ["DANONE", "552032534"],
    "departments": ["75"],
    "nafCodes": ["62.01Z"],
    "status": "active",
    "maxResultsPerQuery": 100
})
items = client.dataset(run["defaultDatasetId"]).list_items().items
print(items)
```

## Pricing

Pay per result — see the current price on the Store page.

## Data source & licence

The data is the Sirene register of INSEE, served by the open API "Recherche d'entreprises" (DINUM), which needs no key. Sirene is published under the Licence Ouverte 2.0 (Etalab), which allows commercial reuse provided that the source and the date of the last update are mentioned. Keep `source`, `sourceLicense` and `sourceUpdatedAt` when you pass the data on, and do not suggest that INSEE, DINUM or the French State endorse your product. This Actor is an independent tool, not an official service; its data is informational and is not a legal extract (no Kbis).

## Support

Open an issue in this repository or use the Issues tab on the Store page.

## Licence

The documentation and examples in this repository are released under the MIT licence (see `LICENSE`). The Actor itself is proprietary and runs on the Apify platform.
