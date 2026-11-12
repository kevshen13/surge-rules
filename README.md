# Surge rules: daily use and independent trading routes

Reviewed: 2026-11-12.

The trading lists are divided by destination service. Applications and their market-data/order providers can choose different exit policies. For example, an application website/license connection may use DIRECT while its CQG connection uses a regional policy.

## Integration order

1. LAN rules and intentional per-device exceptions.
2. `data/`, `brokers/`, and `exchanges/` destination rules.
3. `programs/` domain and process rules.
4. Other service rules, domestic direct routing, and a final daily fallback.

All `.list` files use `RULE-SET`. Data-source rules must precede application process rules. `PROCESS-NAME` applies only to processes on the computer running Surge; a gateway cannot identify processes on another LAN computer. Rules based on destination domains/IPs handle gateway clients.

## Independent lists

| Type | Service | File | Reference |
| --- | --- | --- | --- |
| program | ATAS | [programs/atas.list](programs/atas.list) | [Provider reference](https://atas.net/connections/) |
| program | Ninjatrader | [programs/ninjatrader.list](programs/ninjatrader.list) | [Provider reference](https://developer.ninjatrader.com/) |
| program | Tradovate | [programs/tradovate.list](programs/tradovate.list) | [Provider reference](https://api.tradovate.com/) |
| program | SierraChart | [programs/sierrachart.list](programs/sierrachart.list) | [Provider reference](https://www.sierrachart.com/index.php?l=doc/helpdetails1.php) |
| program | MultiCharts | [programs/multicharts.list](programs/multicharts.list) | [Provider reference](https://www.multicharts.com/) |
| program | Jigsaw | [programs/jigsaw.list](programs/jigsaw.list) | [Provider reference](https://www.jigsawtrading.com/) |
| program | TradingView | [programs/tradingview.list](programs/tradingview.list) | [Provider reference](https://www.tradingview.com/) |
| program | TrendSpider | [programs/trendspider.list](programs/trendspider.list) | [Provider reference](https://trendspider.com/) |
| program | Quantower | [programs/quantower.list](programs/quantower.list) | [Provider reference](https://help.quantower.com/quantower/connections) |
| program | eSignal | [programs/esignal.list](programs/esignal.list) | [Provider reference](https://www.esignal.com/) |
| program | OptimusFlow | [programs/optimusflow.list](programs/optimusflow.list) | [Provider reference](https://optimusflow.com/) |
| program | Medved Trader | [programs/medvedtrader.list](programs/medvedtrader.list) | [Provider reference](https://www.medvedtrader.com/) |
| program | cTrader | [programs/ctrader.list](programs/ctrader.list) | [Provider reference](https://help.ctrader.com/) |
| program | MT5 | [programs/mt5.list](programs/mt5.list) | [Provider reference](https://www.metatrader5.com/en/terminal/help/startworking/settings) |
| data | CQG | [data/cqg.list](data/cqg.list) | [Provider reference](https://help.cqg.com/cqgic/26/Documents/cqgnettechnicalspecifications.htm) |
| data | Rithmic | [data/rithmic.list](data/rithmic.list) | [Provider reference](https://www.rithmic.com/) |
| data | IQFeed | [data/iqfeed.list](data/iqfeed.list) | [Provider reference](https://iqhelp.dtn.com/firewall-ip-addresses/) |
| data | dxFeed | [data/dxfeed.list](data/dxfeed.list) | [Provider reference](https://kb.dxfeed.com/en/getting-started.html) |
| data | Sierra 数据 | [data/sierra-data.list](data/sierra-data.list) | [Provider reference](https://www.sierrachart.com/index.php?l=doc/helpdetails1.php) |
| data | Tradovate 数据 | [data/tradovate-data.list](data/tradovate-data.list) | [Provider reference](https://api.tradovate.com/) |
| data | cTrader 数据 | [data/ctrader-data.list](data/ctrader-data.list) | [Provider reference](https://help.ctrader.com/open-api/proxies-endpoints/) |
| data | TT 数据 | [data/trading-technologies.list](data/trading-technologies.list) | [Provider reference](https://library.tradingtechnologies.com/trade/overview/tt-desktop/description-tt-desktop/tt-desktop-platform-requirements/) |
| broker | Pepperstone | [brokers/pepperstone.list](brokers/pepperstone.list) | [Provider reference](https://pepperstone.com/en/support/platforms-and-tools) |
| broker | IC Markets | [brokers/icmarkets.list](brokers/icmarkets.list) | [Provider reference](https://www.icmarkets.com/global/en/trading-platforms/metatrader-5) |
| broker | Exness | [brokers/exness.list](brokers/exness.list) | [Provider reference](https://get.exness.help/hc/en-us/articles/360012578619-Trading-account-login-and-server-details) |
| exchange | Binance | [exchanges/binance.list](exchanges/binance.list) | [Provider reference](https://developers.binance.com/en/docs/products/spot/rest-api) |
| exchange | OKX | [exchanges/okx.list](exchanges/okx.list) | [Provider reference](https://www.okx.com/docs-v5/en/) |
| exchange | Bybit | [exchanges/bybit.list](exchanges/bybit.list) | [Provider reference](https://bybit-exchange.github.io/docs/v5/ws/connect) |

## Compatibility

The flat filenames remain compatibility aggregates for existing profiles. New configurations should use the individual files above. Existing flat URLs are not a substitute for independently selectable groups.

## Verification and limits

- IQFeed: the documented `12.36.218.128/25` range replaces the old `66.112.149.*` rules. The provider still uses `login.interquote.com`.
- CQG: published ranges and DNS suffixes are included; the provider can change them.
- Sierra data: server addresses follow the current Sierra Chart connection guide. Data/order services under `sierracharts.com` are separated from the `sierrachart.com` application site.
- Rithmic: existing narrow IP ranges are retained and normalized. A current public official firewall advisory could not be retrieved during this review, so the IP portion is explicitly marked as legacy rather than claimed complete.
- MT5: broker-specific servers are not identified by MetaQuotes/MQL5 website rules. Pepperstone publishes MT5 endpoints beneath `pepperstone.com`; IC Markets and Exness account-specific IP-only access points require observed connection details. Do not guess shared-cloud IP blocks.
- cTrader: the data list covers documented `ctraderapi.com` Open API endpoints. Branded desktop clients can use additional access-point names.
- A destination shared by multiple programs receives the same policy unless additional source-device conditions are used.
- Some web platforms combine login, data, and execution on the same hostname. These cannot be distinguished solely by domain routing.
- Routing verification does not log into accounts, submit orders, or prove market-data entitlement.

## Rule-maintenance decisions

- Removed the broad `gemini` AI keyword that also matched the Gemini exchange.
- Removed a whole hosting-provider ASN from the AI list and the non-domain project name `llama.cpp`.
- Existing broker mirrors and unrelated legacy lists were not expanded without a provider reference.
- Public lists contain service domains and provider ranges only; never commit account credentials, subscription URLs, or a full personal Surge profile.

## Third-party integration notes

For blackmatrix7 Apple, AdvertisingLite and GlobalMedia, use the complete `_All_No_Resolve.list` variants supported by current Surge. The short `.list` files omit domain entries and need their companion domain list. [Author instructions](https://github.com/blackmatrix7/ios_rule_script/blob/master/rule/Surge/Apple/README.md).

Put dedicated Google FCM rules before generic Google rules, and Spotify before GlobalMedia. An all-non-CN-TLD proxy list is unnecessary when explicit proxy rules, domestic IP classification and a final proxy fallback already exist.

## Example

```ini
[Rule]
RULE-SET,https://raw.githubusercontent.com/kevshen13/surge-rules/main/data/cqg.list,CQG,no-resolve
RULE-SET,https://raw.githubusercontent.com/kevshen13/surge-rules/main/data/rithmic.list,Rithmic,no-resolve
RULE-SET,https://raw.githubusercontent.com/kevshen13/surge-rules/main/programs/atas.list,ATAS,no-resolve
```

Define the policy groups in the consuming profile; lists do not contain exit choices.
