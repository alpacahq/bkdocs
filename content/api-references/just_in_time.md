---
bookHidden: false
weight: 8
summary: Open brokerage accounts, enable commission-free trading, and manage the ongoing user experience with Alpaca Broker API
title: Just in Time
---

# Just in Time

Just in Time (JIT) Funding enables users to trade without having cash in the account at the time of the trade. Instead, money will be transfered on the day of settlement, or as we like to say, just in time. JIT net settlement utilizes the transfer amount of buying activity less selling activity, which results in lower capital requirements and reduced FX conversion fees. While net settlement is recommended, please reach out to discuss details around gross settlement should that implementation be preferred. 

---

## **The Reports Object**
`GET /v1/transfers/jit/reports`

### Sample Report Object
```json
{
  "report_type": "net_summary",
  "system_date": "2021-07-22"
}
```

### Attributes

| Attribute       | Type               | Requirement   |Notes                                                                                |
| --------------- | ------------------ | ------------- | ------------------------------------------------------------------------------------ |
| `report_type`   | string             | {{<hint danger>}}Required{{</hint>}} | Please view the response table below for a full list of acceptable values. |
| `system_date`   | date               | {{<hint danger>}}Required{{</hint>}} | Must be in YYYY-MM-DD format   |

### Response
Returns one of the following report types using the associated naming convention where 'CORR' is to be replaced with the unique four character alphanumeric code for the correspondent. Note that the Report Type column specifies all valid entries for the `report_type` field in the request above.


| Report Type           | Naming Convention   | Notes                                                                                |
| --------------------- | ------------------ | ------------------------------------------------------------------------------------ |
| `detail`              | CORR-YYYY-MM-DD-detail.csv | Displays all activity across accounts that is factored into the final wire amounts. |
| `net_summary`         | CORR-YYYY-MM-DD-summary.csv | Contains 3 columns, T0, T1, and T2, which specify the net amount due for each trading day. |
| `gross_summary`       | CORR-YYYY-MM-DD-summary.csv | Contains 6 columns, T0, T1, and T2 for 'in' and 'out' amounts respectively which specify the gross amounts due for each trading day. |
| `net_payment`         | CORR-YYYY-MM-DD-payment.pdf | Specifies the net wire amount to be transfered on T+2 as well as the recipient of the wire.  |
| `gross_payment`       | CORR-YYYY-MM-DD-payment.pdf | Specifies the wire amount to be transfered to Alpaca on T+2.  |
| `net_payment_final`   | CORR-YYYY-MM-DD-payment-final.pdf | Shows the final net money movement that accounts for T1 activities that settle T+0 or T+1. |
| `gross_payment_final` | CORR-YYYY-MM-DD-payment-final.pdf | Shows the final gross money movement due to Alpaca that accounts for T1 activities that settle T+0 and T+1.  |

## **The Limits Object**
`GET /v1/tranfers/jit/limits`

### Request
No request body is passed in this endpoint.

### Sample Limits Reponse
```json
{
  "daily_net_limit_in_use": 150000,
  "daily_net_limit": 2000000
}
```

### Attributes

| Attribute                | Type      | Notes             |
| ------------------------ | --------- | ----------------- |
| `daily_net_limit_in_use` | decimal   | The realtime gross buying limit for the current trading day. This is determined by the net amount of buying and selling activity. |
| `daily_net_limit`        | decimal   | The total gross buying limit that can be reached before further buying activity is restricted. |


### Response

{{<hint good>}}**`204`** - Success (No Content){{</hint>}}

---

#### Error Codes

{{<hint warning>}}
400 - Bad Request
_The body in the request is not valid_