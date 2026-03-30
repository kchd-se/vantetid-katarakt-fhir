# CLAUDE.md — Instruktioner för Claude Code

> Denna fil läses automatiskt av Claude Code. Du behöver aldrig förklara dessa regler.
> Filen är identisk i alla paketrepon under kchd-se/.

## Vad är det här?

Ett **distributionspaket** från Vårddatahubben (KCHD, SKR).
Paketspecifik information (namn, version, vårdområde) finns i `manifest.json`.

Regioner ändrar BARA filerna i `vql/01_basvy/`. Allt annat är identiskt för alla regioner.

## Repostruktur — rör inte

```
vql/
├── 00_kodverk/        Referensdata (KVÅ-koder, fas, avvikelser, intervall)
├── 01_basvy/          Interface-vyer — ENDA som regioner anpassar
├── 02_berakning/      Kärnlogik — identisk alla regioner
├── 03_resultatvy/     Färdiga vyer för BI/rapport
└── 04_kvalitet/       Paketspecifika kvalitetskontroller (om tillämpligt)
```

Namnkonvention:
- `ref_*` → 00_kodverk
- `src_*` → 01_basvy
- `calc_*` → 02_berakning
- `res_*` → 03_resultatvy
- `dq_*` → 04_kvalitet

## Branch-modell

- **main** = generisk mall med platshållar-basvyer. Nya regioner utgår härifrån.
- **region/XXX** = regionspecifik gren (t.ex. region/vgr, region/halland).
  Bara filerna i `01_basvy/` skiljer sig från main.

### Regler:

- Buggfixar och ny logik görs ALLTID i **main** först, mergeas sedan till regiongrenar.
- Regionspecifika ändringar (kolumnnamn i basvy) görs direkt i regionens gren.
- Skapa aldrig en regiongren utan att först fråga användaren.

### Merga uppdateringar till en regiongren:

```bash
git checkout region/vgr
git merge main
git push
```

## Versionshantering — följ ALLTID dessa regler

Vi använder **Semantic Versioning (SemVer)**: `MAJOR.MINOR.PATCH`

### VIKTIGT: Ändra ALDRIG version på eget initiativ

Använd exakt den version som anges i prompten. Om ingen version anges — fråga.

### Typer av ändringar:

- **PATCH** (1.0.0 → 1.0.1): Buggfix. Regionen kan uppgradera utan att ändra något.
- **MINOR** (1.0.x → 1.1.0): Ny vy eller kolumn tillagd. Bakåtkompatibelt.
- **MAJOR** (1.x.x → 2.0.0): Kolumn bytt namn/borttagen. Regionen MÅSTE agera.

### Vid VARJE commit som ändrar funktionalitet:

1. Uppdatera CHANGELOG.md
2. Uppdatera manifest.json (version + release_date)
3. Commit-meddelande: `v1.0.1: Kort beskrivning`
4. Skapa git tag: `git tag v1.0.1`
5. Pusha: `git push && git push --tags`

OBS: Om git push --tags blockeras av proxyn, meddela användaren att taggen
behöver skapas manuellt via GitHub Releases.

## Kvalitetskontroll innan release

- [ ] Alla VQL-filer har kommentarsheader med filnamn och version
- [ ] CHANGELOG.md uppdaterad
- [ ] manifest.json har rätt version och datum
- [ ] Git tag matchar version i manifest.json
- [ ] Tester uppdaterade om ny logik lagts till
- [ ] Regiongrenar mergade från main (om tillämpligt)

## Output-aliasnamn är kontrakt

Aliasnamn i resultatvyer läses av nedströms konsumenter (Python, C#, BI-verktyg).
Alias får aldrig ändras utan MAJOR-version.

## Språk

Allt på **svenska**.
