# Warmtepomp en Home Assistant

Blueprints voor de warmtepomp (Technische Alternative UVR610 met C.M.I., aangestuurd via een ESP32 met CoE).
Je kiest alles grafisch in Home Assistant: telefoon, speakers en sensoren.

## Wat erin zit

| Blueprint | Soort | Wat het doet |
| --- | --- | --- |
| `blueprints/script/warmtepomp/melding_warmtepomp.yaml` | Script | Stuurt een melding naar je telefoon, het dashboard en (bij een storing) de speakers. Hier kies je telefoon, speakers, spraakdienst en stille uren. |
| `blueprints/automation/warmtepomp/warmtepomp_meldingen.yaml` | Automation | Stuurt de meldingen van de warmtepomp-ESP door: storingen met advies, C.M.I. onbereikbaar, onderhoud te laat, ESP offline en opgelost. |
| `blueprints/automation/warmtepomp/warmtepomp_woonkamer.yaml` | Automation | Woonkamer (H5): weekschema, toeslag als er iemand thuis is, vakantie; de temperaturen stel je in op het dashboard. Stuurt de gewenste en gemeten temperatuur en "verwarmen toegestaan" naar de ESP. |
| `dashboard/warmtepomp_dashboard.yaml` | Dashboard | Status, meldingen, temperaturen, energie en starts per dag, plus een knop naar de ESP-pagina (werkt thuis). Eerst de helpers uit `dashboard/H3-helpers.md` maken. |
| `dashboard/warmtepomp_tabblad.yaml` | Tabblad | Hetzelfde overzicht als één tabblad, om in een bestaand dashboard te plakken (Bewerken in YAML). |

Later komen erbij: tariefblok (H6), boiler op zon (H7) en koelen (H8).

## Installeren

1. **Helper**: Instellingen > Apparaten en diensten > Helpers > Helper maken > Schakelaar. Naam: `Warmtepomp testfase`.
2. **Blueprints importeren**: Instellingen > Automatiseringen en scènes > Blueprints > Blueprint importeren. Plak de link naar elk bestand op GitHub.
3. **Script maken**: open de blueprint "Warmtepomp: melding versturen", kies je telefoon, speakers en de rest, en sla op als **Melding warmtepomp**.
4. **Automation maken**: open de blueprint "Warmtepomp: meldingen", kies de sensor Melding, de sensor Melding actief en het script uit stap 3, en sla op.

## Woonkamer (H5) installeren

Nodig: ESP-versie H4 of nieuwer.

1. **Helpers**: het weekschema en vier temperaturen, zie `dashboard/H5-helpers.md`.
2. **Blueprint importeren**: de link naar `warmtepomp_woonkamer.yaml` op GitHub.
3. **Automation maken**: open de blueprint "Warmtepomp: woonkamer", controleer de vier temperatuurhelpers, het schema, de personen, de bewegingssensor en de vijf ESP-entiteiten, en sla op als **Warmtepomp woonkamer**.

De UVR doet pas iets met deze signalen na C4 (CAN-ingangen) en C7 (zijn programma). Tot die tijd zie je op de ESP en het dashboard wat Home Assistant zou vragen.

## Bijwerken

Bij een nieuwe versie: Blueprints > drie puntjes bij de blueprint > Blueprint opnieuw importeren. Je keuzes blijven staan.
