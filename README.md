# FHIR-transformering Katarakt — Distributionspaket

Omvandlar resultatvyer från `vantetid-katarakt` till FHIR MeasureReport-format,
från Vårddatahubben (KCHD, SKR).

## Syfte

Detta paket tar resultaten från beräkningspaketet (`vantetid-katarakt`) och
transformerar dem till FHIR R4 MeasureReport-resurser. Vyerna i detta paket
skapar inga egna beräkningar — de läser från `res_kpi_*`-vyerna och mappar
till FHIR-struktur.

## Mappstruktur

```
vql/
├── 02_berakning/      FHIR-transformering (ref_fhir_system, fhir_measure_report)
├── 04_verifiering/    (tom tills vidare)
└── 05_kvalitet/       (tom tills vidare)
tests/                 Testfiler för verifiering
docs/                  Dokumentation
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
3. Kör `vql/02_berakning/fhir_paket.vql` mot er Denodo-instans

## Skapade vyer

| Vy                    | Beskrivning                              |
|-----------------------|------------------------------------------|
| `ref_fhir_system`     | Alla system-URI:er (bytbara)             |
| `fhir_measure_report` | Alla nyckeltal → MeasureReport-rader     |

## Versionshantering

Projektet följer [Semantic Versioning](https://semver.org/lang/sv/).
Se `CHANGELOG.md` för detaljer om ändringar mellan versioner.
