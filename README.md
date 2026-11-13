# Warmtepomp en Home Assistant

Blueprints voor de warmtepomp (Technische Alternative UVR610 met C.M.I., aangestuurd via een ESP32 met CoE).
Je kiest alles grafisch in Home Assistant: telefoon, speakers en sensoren.

## Wat erin zit

| Blueprint | Soort | Wat het doet |
| --- | --- | --- |
| `blueprints/script/warmtepomp/melding_warmtepomp.yaml` | Script | Stuurt een melding naar je telefoon, het dashboard en (bij een storing) de speakers. Hier kies je telefoon, speakers, spraakdienst en stille uren. |
| `blueprints/automation/warmtepomp/warmtepomp_meldingen.yaml` | Automation | Stuurt de meldingen van de warmtepomp-ESP door: storingen met advies, C.M.I. onbereikbaar, onderhoud te laat, ESP offline en opgelost. |

Later komen erbij: dashboard (H3), woonkamer (H5), tariefblok (H6), boiler op zon (H7) en koelen (H8).

## Installeren

1. **Helper**: Instellingen > Apparaten en diensten > Helpers > Helper maken > Schakelaar. Naam: `Warmtepomp testfase`.
2. **Blueprints importeren**: Instellingen > Automatiseringen en scènes > Blueprints > Blueprint importeren. Plak de link naar elk bestand op GitHub.
3. **Script maken**: open de blueprint "Warmtepomp: melding versturen", kies je telefoon, speakers en de rest, en sla op als **Melding warmtepomp**.
4. **Automation maken**: open de blueprint "Warmtepomp: meldingen", kies de sensor Melding, de sensor Melding actief en het script uit stap 3, en sla op.

## Bijwerken

Bij een nieuwe versie: Blueprints > drie puntjes bij de blueprint > Blueprint opnieuw importeren. Je keuzes blijven staan.
