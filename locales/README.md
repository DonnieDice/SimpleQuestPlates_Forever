# /locales

Localization files for SimpleQuestPlates.

## Available Locales

All 12 WoW client locales ship a complete module:

- `enUS.lua` - English baseline/fallback strings (the base table every other locale overrides)
- `enGB.lua` - English (EU) locale module (intentionally enUS-identical values; same language)
- `deDE.lua` - German locale module
- `esES.lua` - Spanish (Spain) locale module (guards `esES` only)
- `esMX.lua` - Mexican Spanish locale module (guards `esMX` only)
- `frFR.lua` - French locale module
- `itIT.lua` - Italian locale module
- `koKR.lua` - Korean locale module
- `ptBR.lua` - Brazilian Portuguese locale module
- `ptPT.lua` - European Portuguese locale module (guards `ptPT` only; does not fall through to ptBR)
- `ruRU.lua` - Russian locale module
- `zhCN.lua` - Simplified Chinese locale module
- `zhTW.lua` - Traditional Chinese locale module

## Guidance

- Add new keys to `enUS.lua` first.
- Every locale module carries the full key set (currently 110 keys) so no key is ever missing at runtime; untranslated-looking keys are a bug, not a fallback.
- Fallback behavior: `enUS.lua` loads first and populates `SQP.L` unconditionally; each other module returns early unless `GetLocale()` matches its guard, so an unmatched client locale or a missing key degrades to the enUS value without Lua errors.
- Keep key names stable to avoid runtime string lookup issues.
- `esMX` and `ptPT` are deliberately separate modules (not shared guards) so each client locale is served by exactly one module.
