# Source Code

The sanitized research scripts will live in this directory.

Before publishing any local trading script, remove or replace:

- MT5 account IDs;
- passwords;
- server credentials;
- API keys;
- personal paths;
- private broker information.

Recommended future layout:

```text
src/
├── baseline_original_reference.py
├── research_runner.py
├── strategies/
│   ├── baseline_sell.py
│   ├── sl245_sell.py
│   └── buy_experiment.py
├── logging/
│   └── trade_logger.py
└── config/
    └── example_config.py
```

Strategy logic should be separated from account configuration so that the repository never requires real credentials.

The upstream strategy source should retain appropriate attribution to its original author and license terms.