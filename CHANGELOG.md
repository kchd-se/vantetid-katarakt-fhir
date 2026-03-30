# Ändringslogg

Alla väsentliga ändringar i detta projekt dokumenteras i denna fil.
Formatet baseras på [Keep a Changelog](https://keepachangelog.com/sv/1.0.0/)
och projektet följer [Semantic Versioning](https://semver.org/lang/sv/).

## [1.0.0] — 2026-03-30

### Tillagt
- Initial projektstruktur för FHIR-transformering
- fhir_paket.vql v3.1 i vql/02_berakning/ — komplett FHIR-mappning
- ref_fhir_system: Alla system-URI:er (KVÅ, ICD-10-SE, HSA-ID, Measure-URL:er)
- fhir_measure_report: 16 KPI:er × alla dimensioner som MeasureReport-rader
- Stöd för andel inom 90d, median, medel, patientresa, remiss→beslut
- Per-dimension-stratifiers: yrkeskategori, kontaktform, bokning, remittent, kommun
- CLAUDE.md med instruktioner för Claude Code
- manifest.json för versionshantering och regionspårning
- README.md med projektdokumentation
