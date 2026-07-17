# Sample Data

This directory is reserved for small, anonymized datasets that allow contributors to reproduce selected analyses without exposing private MT5 account information.

Recommended fields for trade-level samples:

- trade_id (anonymized);
- experiment_id / magic_number;
- entry_time;
- exit_time;
- side;
- entry_type (FIRST/ADD);
- entry_price;
- exit_price;
- volume;
- tp;
- sl;
- realized_pnl;
- exit_reason;
- MAE;
- MFE;
- relevant indicator values.

Do not upload account numbers, passwords, personal names, or unnecessary broker-specific identifiers.

Large raw market-history files should generally not be committed directly to Git unless there is a clear reproducibility need and an appropriate storage strategy.