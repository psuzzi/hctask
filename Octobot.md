# Octobot

Clone, setup, run and stop Octobot.

```bash
git clone git@github.com:psuzzi/Python-Trading-Website.git && cd $_
python3.10 -m venv venv #first time
source venv/bin/activate #dev time
pip install -r requirements.txt #first time
python start.py #run
deactivate #stop
```

Note: found an error while installing requirements. 
- asked on discord, see [this](https://discord.com/channels/530629985661222912/530636611222765593/1288550451029086289)
- solution: use Python 3.10 instead of 3.12, see [this issue](https://github.com/Drakkar-Software/OctoBot/issues/2678#issuecomment-2231294572) 

as a result: `python3.10 ..` instead of `python -m venv venv`, and it works





## start

When starting the Octobot initializes, loads configuratons, installs tentacles (modules), starts a web interface, and begins simulated trading. Several services attempt to initialize, but some fail due to configuration issues.

### first run

when running `python start.py` 
- the Octobot 2.0.5 starts in a self-hosted environment, and you see logs
  - the bot tries to load conf, but none is found and creates a new one
  - a disclaimer about risks is logged
  - tentacles installation 
    - several tentacles installed, incl evaluators (trend_analysis, statistic_analysis), backtesting tools, trading strategies, (e.g. DCA, arbitrage_trading), and service integrations (e.g. telegram_service, wen_service)
    - tentacles related to market data collection (e.g. from binance and other exch.) are also installed
  - Profiles update: 
    - the bot updates various trading profiles, e.g. Non-Trading, Signal Trading, GPT Trading, Grid Trading, Daily Trading, etc. Profiles seem to define different trading modes/strategies.
  - Starting web interface
    - A web service is started, accessible at http://192.168.1.4:5001
      - This is a UI for managing / monitoring the bot
      - a disclaimer about risks is shown
  - Service Initialization:
    - Several services are attempted to be initialized, incl. Binance, and some other integrations like GoogleServiceFeed, RedditService, and TelegramService
  - Simulated Trading:
    - The bot starts in simulated trading mode on the Binance exch., trading the BTC/USDT pair. (So no real trades are executed, but it simulates market activity for testing)

### Python Services/Classes

- `octobot.cli.main(argv[1:])`: main entry point
- `octobot_parser`: CLI parser

- Tentacles: the core modular components used by the bot, including
  - Evaluator.Util, Evaluator.TA, Trading.Exchange, Trading.Mode, Service.Services_bases, etc.
  - Tentacles representing analysis tools, trading strategies, exchange connectors, and services like Telegram, Web, and GPT integration
- WebService: provides the web interface running at http://192.168.1.4:5001
- ServiceFactory: Used to initialize services like RedditService, WebHookService, and TelegramService. Some services fail to initialize due to invalid configurations
- CCXTConnector: used to manage connections to exchanges (e.g. Binance)