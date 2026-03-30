# FHIR-transformering Katarakt — Distributionspaket

Omvandlar resultatvyer från `vantetid-katarakt` till FHIR R4 MeasureReport-format
via en C#/Python-pipeline, från Vårddatahubben (KCHD, SKR).

## Syfte

Detta paket tar resultaten från beräkningspaketet (`vantetid-katarakt`) och
transformerar dem till FHIR R4 MeasureReport-resurser. Pipelinen består av:

- **VQL** — vyer i Denodo som mappar beräknade KPI:er till FHIR-struktur
- **C#** — FHIR-serialisering med Firely SDK

## Mappstruktur

```
csharp/                C#-pipeline (FHIR-serialisering)
vql/                   VQL-vyer för FHIR-mappning (Denodo)
```

## Beroenden

Paketet förutsätter att följande vyer redan finns (från `vantetid-katarakt`):

- `res_kpi_manad`
- `res_kpi_per_yrke`
- `res_kpi_per_kontaktform`
- `res_kpi_per_bokning`
- `res_kpi_per_remittent`
- `res_kpi_per_kommun`

## Kom igång

1. Installera först `vantetid-katarakt` och kör dess VQL-filer
2. Klona detta repo
3. Kör VQL-vyerna i `vql/` mot er Denodo-instans
4. Bygg och kör C#-pipelinen i `csharp/`

## Versionshantering

Projektet följer [Semantic Versioning](https://semver.org/lang/sv/).
Se `CHANGELOG.md` för detaljer om ändringar mellan versioner.
