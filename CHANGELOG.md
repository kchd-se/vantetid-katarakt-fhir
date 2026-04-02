# Ändringslogg

Alla väsentliga ändringar i detta projekt dokumenteras i denna fil.
Formatet baseras på [Keep a Changelog](https://keepachangelog.com/sv/1.0.0/)
och projektet följer [Semantic Versioning](https://semver.org/lang/sv/).

## [1.0.1] — 2026-04-02

### Tillagt
- Ny parameter `--schema` för att prefixera vynamnet med Denodo-schema
- VGR kan nu köra: `KchdFhirSerializer.exe --odbc "DSN=DenodoODBC-dev" --schema Datamart_Tillgänglighet`

### Fixat
- Kolumnnamn från ODBC/TSV matchas nu case-insensitive (förhindrar tyst fel om Denodo returnerar versaler)
- Dimension-stratifiers hamnar nu på rätt group baserat på group_code (inte alltid group[0])
- Default rapportdatum är nu dagens datum istället för hårdkodat 2026-03-26
- Explicit hantering av NULL/None/NaN-strängar i measure_score-parsning
- ODBC-anslutningsfel ger nu tydligt felmeddelande med felsökningsinstruktioner
- ODBC CommandTimeout satt till 5 minuter (förhindrar timeout vid tunga vyer)

### Borttaget
- appsettings.json (användes aldrig, vilseledande)

### Dokumentation
- Dokumenterat krav på 64-bit ODBC DSN i README
- Dokumenterat UTF-8 charset-krav för Denodo ODBC-drivrutin

## [1.0.0] — 2026-03-30

### Tillagt
- Initial projektstruktur för FHIR-transformering med C#/Python-pipeline
- Mappstruktur: csharp/, vql/
- fhir_paket.vql v3.1 i vql/ — komplett FHIR-mappning
- ref_fhir_system: Alla system-URI:er (KVÅ, ICD-10-SE, HSA-ID, Measure-URL:er)
- fhir_measure_report: 16 KPI:er × alla dimensioner som MeasureReport-rader
- Stöd för andel inom 90d, median, medel, patientresa, remiss→beslut
- Per-dimension-stratifiers: yrkeskategori, kontaktform, bokning, remittent, kommun
- CLAUDE.md med instruktioner för Claude Code
- manifest.json för versionshantering och regionspårning
- README.md med projektdokumentation
