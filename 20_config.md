<!-- Space: OP -->
<!-- Parent: Operational Readiness Review -->
<!-- Title: OPR - Configuration -->

# Config

- Layered config (CLI args > env > config file (if >1 config file define order explicitly and document)
- Config should be “batteries included” - your application should have as few mandatory config values as possible (outside of secrets) by having okay defaults for everything
- Default values should, where possible, prefer something that is likely to work in a variety of environments over something that is optimal in a few
- Not including defaults is a valid strategy where the risk of misconfiguration is high. An application that doesn’t start is preferable to one that starts and then demolishes your database.
