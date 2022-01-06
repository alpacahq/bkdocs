---
bookHidden: false
weight: 1
title: "Entity Account"
summary: Open brokerage accounts, enable commission-free trading, and manage the ongoing user experience with Alpaca Broker API
---

# Accounts

The entity accounts API allows you to create and manage the accounts under an entity, a person or legal body that oversees accounts.

## **Allowed Setups**

{{<hint danger>}}**Non-Disclosed:** Brokers with an ND setup cannot access the Accounts API{{</hint>}}

---

## **The Entity Account Model**

### Sample Account Object

```json
{
  "contact": {
    "email_address": "trustee@apple.com",
    "phone_number": "408-996-1010",
    "street_address": "One Apple Way",
    "city": "Cupertino",
    "state": "CA",
    "postal_code": "95014",
    "country": "USA"
  },
  "identity": {
    "given_name": "John",
    "family_name": "Doe",
    "date_of_birth": "01/17/1965",
    "tax_id": "123-45-6789",
    "tax_id_type": "US_SSN",
    "country_of_citizenship": "USA",
    "country_of_birth": "USA",
    "country_of_tax_residence": "USA",
    "funding_source": ["investments"]
  },
  "disclosures": {
    "is_control_person": false,
    "is_affiliated_exchange_or_finra": false,
    "is_politically_exposed": false,
    "immediate_family_exposed": false
  }
}
```

### Attributes

#### Parameters

| Attribute         | Notes                                                                                        |
| ----------------- | -------------------------------------------------------------------------------------------- |
| `contact`         | Contact information about the user                                                           |
| `identity`        | KYC information about the user                                                               |
| `disclosures`     | Required disclosures about the user                                                          |

**Contact**

| Attribute        | Type   |
| ---------------- | ------ |
| `email_address`  | string |
| `phone_number`   | string |
| `street_address` | array  |
| `city`           | string |
| `state`          | string |
| `postal_code`    | string |

**Identity**

| Attribute                    | Type                                                            |
| ---------------------------- | --------------------------------------------------------------- |
| `given_name`                 | string                                                          |
| `family_name`                | string                                                          |
| `date_of_birth`              | date                                                            |
| `tax_id`                     | string                                                          |
| `tax_id_type`                | [ENUM.TaxIdType]({{< relref "#tax-id-type" >}})                 |
| `country_of_citizenship`     | string                                                          |
| `country_of_birth`           | string                                                          |
| `country_of_tax_residence`   | string                                                          |
| `visa_type`                  | [ENUM.VisaType]({{< relref "#visa-type" >}})                    |
| `visa_expiration_date`       | date                                                            |
| `date_of_departure_from_usa` | date                                                            |
| `permanent_resident`         | boolean                                                         |
| `funding_source`             | array of [ENUM.FundingSource]({{< relref "#funding-source" >}}) |
| `annual_income_min`          | string/number                                                   |
| `annual_income_max`          | string/number                                                   |
| `liquid_net_worth_min`       | string/number                                                   |
| `liquid_net_worth_max`       | string/number                                                   |
| `total_net_worth_min`        | string/number                                                   |
| `total_net_worth_max`        | string/number                                                   |
| `extra`                      | object                                                          |

**Disclosures**

It is your responsibility as the service provider to denote if the account owner falls under each category defined by FINRA rules. We recommend asking these questions at any point of the onboarding process of each account owner in the form of Y/N and Radio Buttons.

| Attribute                         | Type                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| `is_control_person`               | boolean                                                      |
| `is_affiliated_exchange_or_finra` | boolean                                                      |
| `is_politically_exposed`          | boolean                                                      |
| `immediate_family_exposed`        | boolean                                                      |
| `employment_status`               | [ENUM.EmploymentStatus]({{< relref "#employment-status" >}}) |
| `employer_name`                   | string                                                       |
| `employer_address`                | string                                                       |
| `employment_position`             | string                                                       |

### Enums

#### Tax ID Type

| Attribute       | Description                            |
| --------------- | -------------------------------------- |
| `USA_SSN`       | USA Social Security Number             |
| `ARG_AR_CUIT`   | Argentina CUIT                         |
| `AUS_TFN`       | Australian Tax File Number             |
| `AUS_ABN`       | Australian Business Number             |
| `BOL_NIT`       | Bolivia NIT                            |
| `BRA_CPF`       | Brazil CPF                             |
| `CHL_RUT`       | Chile RUT                              |
| `COL_NIT`       | Colombia NIT                           |
| `CRI_NITE`      | Costa Rica NITE                        |
| `DEU_TAX_ID`    | Germany Tax ID (Identifikationsnummer) |
| `DOM_RNC`       | Dominican Republic RNC                 |
| `ECU_RUC`       | Ecuador RUC                            |
| `FRA_SPI`       | France SPI (Reference Tax Number)      |
| `GBR_UTR`       | UK UTR (Unique Taxpayer Reference)     |
| `GBR_NINO`      | UK NINO (National Insurance Number)    |
| `GTM_NIT`       | Guatemala NIT                          |
| `HND_RTN`       | Honduras RTN                           |
| `HUN_TIN`       | Hungary TIN Number                     |
| `IDN_KTP`       | Indonesia KTP                          |
| `IND_PAN`       | India PAN Number                       |
| `ISR_TAX_ID`    | Israel Tax ID (Teudat Zehut)           |
| `ITA_TAX_ID`    | Italy Tax ID (Codice Fiscale)          |
| `JPN_TAX_ID`    | Japan Tax ID (Koijin Bango)            |
| `MEX_RFC`       | Mexico RFC                             |
| `NIC_RUC`       | Nicaragua RUC                          |
| `NLD_TIN`       | Netherlands TIN Number                 |
| `PAN_RUC`       | Panama RUC                             |
| `PER_RUC`       | Peru RUC                               |
| `PRY_RUC`       | Paraguay RUC                           |
| `SGP_NRIC`      | Singapore NRIC                         |
| `SGP_FIN`       | Singapore FIN                          |
| `SGP_ASGD`      | Singapore ASGD                         |
| `SGP_ITR`       | Singapore ITR                          |
| `SLV_NIT`       | El Salvador NIT                        |
| `SWE_TAX_ID`    | Sweden Tax ID (Personnummer)           |
| `URY_RUT`       | Uruguay RUT                            |
| `VEN_RIF`       | Venezuela RIF                          |
| `NOT_SPECIFIED` | Other Tax IDs                          |

- Please feel free to reach out to Alpaca if you need other tax ID types.

#### Funding Source

| Attribute           | Description       |
| ------------------- | ----------------- |
| `employment_income` | Employment income |
| `investments`       | Investments       |
| `inheritance`       | Inheritance       |
| `business_income`   | Business income   |
| `savings`           | Savings           |
| `family`            | Family            |

#### Visa Type

In addition to the following USA visa categories, we accept any sub visas of the list below. Sub visas must be passed in according to their parent category. Note that United States green card holders are considered permanent residents and should not pass in a visa type.

| Attribute | Description                 |
| --------- | --------------------------- |
| `B1`      | USA Visa Category B-1       |
| `B2`      | USA Visa Category B-2       |
| `DACA`    | USA Visa Category DACA      |
| `E1`      | USA Visa Category E-1       |
| `E2`      | USA Visa Category E-2       |
| `E3`      | USA Visa Category E-3       |
| `F1`      | USA Visa Category F-1       |
| `G4`      | USA Visa Category G-4       |
| `H1B`     | USA Visa Category H-1B      |
| `J1`      | USA Visa Category J-1       |
| `L1`      | USA Visa Category L-1       |
| `Other`   | Any other USA Visa Category |
| `O1`      | USA Visa Category O-1       |
| `TN1`     | USA Visa Category TN-1      |

#### Employment Status

| Attribute    | Description |
| ------------ | ----------- |
| `unemployed` | Unemployed  |
| `employed`   | Employed    |
| `student`    | Student     |
| `retired`    | Retired     |

---

## **Creating an Entity Account**

Submit an entity account application by filling out the Entity Account Model with the relevant information to Alpaca's team. From there, proper KYC / KYB checks will occur before the account becomes active.


### Request

##### Sample Request Body

```json
{
  "contact": {
    "email_address": "trustee@apple.com",
    "phone_number": "408-996-1010",
    "street_address": "One Apple Way",
    "city": "Cupertino",
    "state": "CA",
    "postal_code": "95014",
    "country": "USA"
  },
  "identity": {
    "given_name": "John",
    "family_name": "Doe",
    "date_of_birth": "01/17/1965",
    "tax_id": "123-45-6789",
    "tax_id_type": "US_SSN",
    "country_of_citizenship": "USA",
    "country_of_birth": "USA",
    "country_of_tax_residence": "USA",
    "funding_source": ["investments"]
  },
  "disclosures": {
    "is_control_person": false,
    "is_affiliated_exchange_or_finra": false,
    "is_politically_exposed": false,
    "immediate_family_exposed": false
  }
}
```

#### Parameters

| Attribute         | Requirement                                          | Notes                                      |
| ----------------- | ---------------------------------------------------- | ------------------------------------------ |
| `contact`         | {{<hint danger>}}Required {{</hint>}}                |                                            |
| `identity`        | {{<hint danger>}}Required {{</hint>}}                |                                            |
| `disclosures`     | {{<hint danger>}}Required {{</hint>}}                |                                            |

**Contact**

| Attribute        | Type   |  Requirement                          |Notes                                                                      |
| ---------------- | ------ | ------------------------------------- | ------------------------------------------------------------------------- |
| `email_address`  | string | {{<hint danger>}}Required {{</hint>}} |                                                                           |
| `phone_number`   | string | {{<hint danger>}}Required {{</hint>}} | _Phone number should include the country code, format: "+15555555555"_    |
| `street_address` | string | {{<hint danger>}}Required {{</hint>}} |                                                                           |
| `city`           | string | {{<hint danger>}}Required {{</hint>}} |                                                                           |
| `state`          | string | {{<hint danger>}}Required{{</hint>}}    |
| `postal_code`    | string | {{<hint danger>}}Required {{</hint>}}   |                                              

**Identity**

| Attribute                    | Type                                                   | Requirement                           | Notes                                                                                   |
| ---------------------------- | ------------------------------------------------------ | ------------------------------------- | --------------------------------------------------------------------------------------- |
| `given_name`                 | string                                                 | {{<hint danger>}}Required {{</hint>}} |                                                                                       |
| `family_name`                | string                                                 | {{<hint danger>}}Required {{</hint>}} |                                                                                       |
| `date_of_birth`              | date                                                   | {{<hint danger>}}Required {{</hint>}}  |                                                                                       |
| `tax_id`                     | string                                                 | {{<hint danger>}}Required {{</hint>}}   | Required for trading accounts if `tax_id_type` is set. 3 letter country code acceptable.             |
| `tax_id_type`                | [ENUM.TaxIdType]({{< relref "#tax-id-type" >}})        | {{<hint info>}}Optional {{</hint>}}   |      |
| `country_of_citizenship`     | string                                                 | {{<hint info>}}Optional {{</hint>}}   |      |
| `country_of_birth`           | string                                                 | {{<hint info>}}Optional {{</hint>}}   |      |
| `country_of_tax_residency`   | string                                                 | {{<hint info>}}Optional {{</hint>}} |        |
| `visa_type`                  | [ENUM.VisaType]({{< relref "#visa-type" >}})           | {{<hint info>}}Optional {{</hint>}}   | Only used to collect visa types for users residing in the USA.                                                              |
| `visa_expiration_date`       | date                                                   | {{<hint info>}}Optional {{</hint>}}   | Required if `visa_type` is set.                                                                                    |
| `date_of_departure_from_usa` | date                                                   | {{<hint info>}}Optional {{</hint>}}   | Required if `visa_type` = `B1` or `B2`.                                                                                   |
| `permanent_resident`         | boolean                                                | {{<hint info>}}Optional {{</hint>}}   | Only used to collect permanent residence status in the USA.                                                            |
| `funding_source`             | [ENUM.FundingSource]({{< relref "#funding-source" >}}) | {{<hint danger>}}Optional {{</hint>}} |                                                                                       |
| `annual_income_min`          | string/number                                          | {{<hint info>}}Optional {{</hint>}}   |                                                             |
| `annual_income_max`          | string/number                                          | {{<hint info>}}Optional {{</hint>}}   |                                                             |
| `liquid_net_worth_min`       | string/number                                          | {{<hint info>}}Optional {{</hint>}}   |                                                             |
| `liquid_net_worth_max`       | string/number                                          | {{<hint info>}}Optional {{</hint>}}   |                                                             |
| `total_net_worth_min`        | string/number                                          | {{<hint info>}}Optional {{</hint>}}   |                                                                                       |
| `total_net_worth_max`        | string/number                                          | {{<hint info>}}Optional {{</hint>}}   |                                                                                       |
| `extra`                      | object                                                 | {{<hint info>}}Optional {{</hint>}}   |  Any additional information used for KYC purposes.                                                                       |

**Disclosures**

It is your responsibility as the service provider to denote if the account owner falls under each category defined by FINRA rules. We recommend asking these questions at any point of the onboarding process of each account owner in the form of Y/N and Radio Buttons.

| Attribute                         | Type                                                         | Requirement                           | Notes                           |
| --------------------------------- | ------------------------------------------------------------ | ------------------------------------  | ------------------------------------- |
| `is_control_person`               | boolean                                                      | {{<hint danger>}}Required {{</hint>}} | Whether user holds a controlling position in a publicly traded company, member of the board of directors or has policy making abilities in a publicly traded company.    |
| `is_affiliated_exchange_or_finra` | boolean                                                      | {{<hint danger>}}Required {{</hint>}} |                                   |
| `is_politically_exposed`          | boolean                                                      | {{<hint danger>}}Required {{</hint>}}  |                                   |
| `immediate_family_exposed`        | boolean                                                      | {{<hint danger>}}Required {{</hint>}} | If your user’s immediate family member (sibling, husband/wife, child, parent) is either politically exposed or holds a control position.                            |
| `employment_status`               | [ENUM.EmploymentStatus]({{< relref "#employment-status" >}}) | {{<hint info>}}Optional {{</hint>}}   |                                   |
| `employer_name`                   | string                                                       | {{<hint info>}}Optional {{</hint>}}   |                                   |
| `employer_address`                | string                                                       | {{<hint info>}}Optional {{</hint>}}   ||                                   |
| `employment_position`             | string                                                       | {{<hint info>}}Optional {{</hint>}}   |                                   |

### Response

Alpaca will manually send you the resulting `entity_id` for future use .

---

## **Creating a Non-Disclosed Account**

`POST /v1/accounts/`

Currently, supported account types include `trading`, `donor_advised`, and `trust`.

### Request

#### Sample Request Body

```json
{
  "entity_id": "<entity_id>",
  "account_type": "donor_advised",
}
```

#### Parameters

| Attribute      | Requirement                           |
| -------------- | ------------------------------------- |
| `entity_id`    | {{<hint danger>}}Required {{</hint>}} |
| `account_type` | {{<hint danger>}}Required {{</hint>}} |

#### Sample Response Body

```json
{
  "id": "<account_id>",
  "account_number": "<account_number>",
  "status": "ACTIVE",
  "currency": "USD",
  "last_equity": "0",
  "created_at": "<current_time>",
  "account_type": "donor_advised"
}
```


&nbsp;
