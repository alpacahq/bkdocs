---
bookHidden: false
weight: 5
summary: Open brokerage accounts, enable commission-free trading, and manage the ongoing user experience with Alpaca Broker API
---

# Trading Configurations

## The Configuration Object

### Sample Object

```json
{
  "dtbp_check": "entry",
  "fractional_trading": true,
  "max_margin_multiplier": "1",
  "no_shorting": false,
  "pdt_check": "entry",
  "suspend_trade": false,
  "trade_confirm_email": "all"
}
```

### Attributes

| Attribute               | Type          | Notes                                                                       |
| ----------------------- | ------------- | --------------------------------------------------------------------------- |
| `dtbp_check`            | string        | `both`, `entry`, or `exit`. Controls Day Trading Margin Call (DTMC) checks. |
| `fractional_trading`    | boolean       | If true, account is able to participate in fractional trading               |
| `max_margin_multiplier` | string/number | Can be `1` or `2` or `4` see "Setting Max Margin Multiplier" below                                                          |
| `no_shorting`           | boolean       | If true, account becomes long-only mode.                                    |
| `pdt_check`             | string        |                                                                             |
| `suspend_trade`         | boolean       | If true, new orders are blocked.                                            |
| `trade_confirm_email`   | string        | `all` or `none`. If `none`, emails for order fills are not sent.            |

---

## Setting Max Margin Multiplier

The margin given to an account is min(max_margin_multiplier, system_calculated_margin). The system_calculated_margin is 1 for accounts with assets less than $2k USD, 2 for accounts with between $2k USD - $25k USD and 4 for accounts with assets over $25k USD.

`PATCH/v1/trading/accounts/{account_id}/account/configurations`

### Request

#### Sample Request

```json
{
  "max_margin_multiplier": 1.0
}
```

### Response

Response will contain the account configuration settings for the account.

&nbsp;
