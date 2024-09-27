# Task

## Understand


- Add wallet connect feature
- after connect, display list of cryptos available for trading 

## Reproduce 


To reproduce the starting point
- install deps, and start.py, see [Octobot](Octobot.md))
- open http://192.168.1.4:5001/profile 

## Solution


### Main idea:
changes both b/e anf f/e:
- FE
  - add wallet connect button
  - implement wallet connect button to handle connection to popular walls, e.g. metamask
  - fetch wallet cryptos
- BE
  - update backend to accept and store the list of pryptos from the connected wallet
- FE
  - update the frontend to display the list of cryptos from the connected walled, instead of just BTC


#### Step one

profile.html: Add Wallet Connect button
configuration.js: add handle_connect_wallet_button()
config.py: add routed connect_wallet() 

The existing buttons can help, e.g. 
- Connect, wallet-connect-button, handle_connect_wallet_button, /connect_wallet
- Export, export-currencies-button, handle_export_currencies_button, /get_config_currency
- Import, import-currencies-button, handle_import_currencies, set_config_currency
- ADD, AddCurrency, 