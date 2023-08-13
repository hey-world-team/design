# Design a "Currency converter service"

## Functional Requirements:

Service provides a list of best chains for exchange from source currency (SC) to target currency (TC) through a p2p buy/sell intermediate crypto coins (ICC) in the crypto exchange (CE).

Supports source/target currencies:
- RUB
- EUR
- USD

Supports intermediate crypto coins:
- USDT
- ETH
- BTC

Supports crypto exchange:
- ByBit
- Binance

Prices of ICC p2p received by request to API of CE. Prices of SC/TC received by request to API of Bank in a country(ies) of currency:
- RUB - Russia
- EUR - Europe
- USD - USA

## Non-functional Requirements:

Performance:
- The website should load on users' screens within 1 second.
- The database queries should not take longer than 100 milliseconds to execute.

Security:
- Service doesn't store any information except cookies for providing a history of converting.

Consistency: Eventual (Read-your-writes consistency)
- System doesn't guarantee on-demand providing requested data but guarantees their delivery.

Scalability:
- The system must be able to handle a 50% increase in user load during peak hours without degradation in performance.
- The application should support adding additional server nodes to accommodate growing user demand.

Reliability:
- The system should have an uptime of at least 99.9% over a one-year period.
- The software should automatically recover and resume operation in case of unexpected crashes.

Availability:
- The service should have a chatbot with FAQ.
- Maintenance downtime should be scheduled during off-peak hours to minimize disruption.

Usability:
- The user interface should be intuitive and easy to navigate.
- The main page should have one button for requesting a list of chains.
- Every answer window has a copy button for copying content to the buffer.
- The system should be accessible to users with disabilities, following WCAG 2.0 accessibility guidelines.

Estimations:
- 100k users per day;
- 20 requests per user;
- 100k * 20 / 86400 = 23 views/day

## API:

### Get Best Chain List

Provides a list of chains of the best way to converting by: buy ICC for SC -> buy TC for ICC

Parameters/Headers:
- Count of chains - not required - by default 20
- % successfully trades of trader - not required - by default 98
- Only verified - not required - false
- CE name - not required - by default all CE
- SC - required - RUB/EUR/USD
- TC - required - RUB/EUR/USD
- ICC - not required USDT/BTC/ETH

Chain:
````
CE name:
    { 
        chain 1....chain n :
            { 
                order 1 ... order n :
                { 
                    trader name of buyer:
                        { 
                            info about trader
                        },
                    price of order - buy ICC for SC,
                    trader name of seller:
                        {
                            info about trader
                        },
                    price of order - sell ICC for TC
                }
            }
    }
````