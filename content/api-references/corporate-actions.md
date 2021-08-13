---
bookHidden: false
weight: 5
summary: Open brokerage accounts, enable commission-free trading, and manage the ongoing user experience with Alpaca Broker API
---

# Corporate Actions

This API endpoint offers the ability to retrieve historical corporate action announcements. There are four primary types of corporate action announcements which can be defined as follows.

- Dividend: a sum of money paid regularly, typically quarterly, by a company to its shareholders out of its profits or reserves
- Merger: the combination of a parent and child company into one larger entity
- Spinoff: the creation of an independent company through the sale or distribution of new shares of an existing business or division of a parent company
- Split: a division of existing shares of a company's stock into multiple new shares resulting in a change in price and shareholder quantity
  - Reverse Split: a subtype of a standard stock split in which a company is merging multiple stocks into one

---
## **The Announcement Object**

### Sample Object

``` json
[
  {
   "ca_type": "Dividend",
    "ca_sub_type": "DIV",
    "initiating_symbol": "MLLAX",
    "initiating_original_cusip": "55275E101",
    "target_symbol": "MLLAX",
    "target_original_cusip": "55275E101",
    "declaration_date": "2021-01-05",
    "expiration_date": "2021-01-12",
    "record_date": "2021-01-13",
    "payable_date": "2021-01-14",
    "cash": "0.018",
    "old_rate": "1",
    "new_rate": "1"
  },
  {
   "ca_type": "Merger",
    "ca_sub_type": "Merger Completion",
    "initiating_symbol": "CRM",
    "initiating_original_cusip": "79466L302",
    "target_symbol": "WORK",
    "target_original_cusip": "83088V102",
    "declaration_date": "2021-07-21",
    "expiration_date": "2021-07-21",
    "record_date": "2021-07-21",
    "payable_date": "2021-07-21",
    "cash": "26,79",
    "old_rate": "1",
    "new_rate": "0.078"
  }
]
```

### Attributes

| Attribute                   | Type          | Description                                                                       |
| --------------------------- | ------------- | --------------------------------------------------------------------------------- |
| `ca_type`                   | string        | Corporate action announcement type                                                |
| `ca_sub_type`               | string        | Subtype of the corporate action announcement                                      |
| `initiating_symbol`         | string        | Optional: Symbol of the parent company (for merger, spinoff, and reorg)           |
| `initiating_original_cusip` | string        | Optional: CUSIP of the parent company (for merger, spinoff, and reorg)            |
| `target_symbol`             | string        | Optional: Symbol of the child company (for merger, spinoff, and reorg)            |
| `target_original_cusip`     | string        | Optional: CUSIP of the child company (for merger, spinoff, and reorg)             |
| `declaration_date`          | string/date   | Date that the corporate action is announced                                       |
| `expiration_date`           | string/date   | The first trade date that shares are excluded from the entitlement                |
| `record_date`               | string/date   | The latest date the shares can settle to receive any entitlments                  |
| `payable_date`              | string/date   | Transaction date for the entitlements of the shareholder                          |
| `cash`                      | string/number | The amount of cash per share to be credited to the shareholder's account          |
| `old_rate`                  | string/number | Previous value of the share after the entitlement                                 |
| `new_rate`                  | string/number | Current value of the share after the entitlement                                  |

---

## **Retrieving Corporate Action Announcements**

`GET /v1/corporate_actions/announcements`

### Request

#### Sample Request

```json
{
  "since": "2021-01-01",
  "until": "2021-01-31",
  "ca_types": "Dividend,Merger",
  "date_type": "payable_date",
  "symbol": null,
  "cusip": null
}
```

#### Parameters

| Attribute  | Type             | Requirement                         | Notes                                                                |
| ---------- | ---------------- | ----------------------------------- | -------------------------------------------------------------------- |
| `ca_types` | string           | {{<hint info>}}Required {{</hint>}} | Comma-delimited string list                                          |
| `since`    | string/timestamp | {{<hint info>}}Required {{</hint>}} | The first date to retrieve data for (inclusive) in YYYY-MM-DD format |
| `until`    | string/timestamp | {{<hint info>}}Required {{</hint>}} | The last date to retrieve data for (inclusive) in YYYY-MM-DD format  |
| `symbol`   | string           | {{<hint info>}}Optional {{</hint>}} |                                                                      |
| `cusip`    | string           | {{<hint info>}}Optional {{</hint>}} |                                                                      |
| `date_type`| string           | {{<hint info>}}Optional {{</hint>}} |                                                                      |

### Response

An array of announcement objects.

---

## **Constraints and Error Codes**

### Constraints

In order to preserve the integrity of Alpaca’s database performance for all users, the ca_type, since, and until fields are required. Please note that it is acceptable to pass in all five corporate action types in the form a list of strings. Additionally, the limit on the length of the date range interval is 90 day intervals per API call, however, you may make multiple calls of 90 day blocks should the need arise to capture corporate action announcements over a longer time frame. Should an invalid date range be passed that breaks these limitations, the following error message will occur.

### Error Codes

{{<hint warning>}}
400 - Bad Request

​ _The body in the request is not valid._
{{</hint>}}

{{<hint warning>}}
401 - Authorization

​ _Request is not authorized._
{{</hint>}}

{{<hint warning>}}
422 - Bad Request

​ _Invalid input value._
{{</hint>}}

{{<hint warning>}}
500 - Internal Server Error

​ _Some server error occurred. Please contact Alpaca_
{{</hint>}}
