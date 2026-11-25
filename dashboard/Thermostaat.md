# Thermostaat woonkamer

Een ronde thermostaat op het dashboard, zoals de RAS, met vier standen:

| Stand | Wat er gebeurt | De draaiknop |
| --- | --- | --- |
| **Automatisch** | Het weekschema: comfort, laag en de toeslag als er iemand thuis is | Toont wat HA vraagt. Draai je eraan, dan gaat de stand naar **Handmatig** met die temperatuur, tot je zelf weer Automatisch kiest |
| **Handmatig** | Eén vaste temperatuur, dag en nacht, zonder schema en toeslag | De knop is de vaste temperatuur |
| **Koelen** | Koelvraag aan, verwarmen uit | Toont wat HA vraagt |
| **Vakantie** | De vakantietemperatuur | De knop is de vakantietemperatuur |

Onder de knop staat **HA vraagt nu**, met de reden. Tik op het icoon naast de kop Woonkamer voor **Instellingen**: comfort, laag, toeslag en vakantietemperatuur.

De thermostaat stuurt zelf niets aan. De automatisering **Warmtepomp woonkamer** blijft de temperatuur bepalen en naar de controller sturen.

## 1. Het package plaatsen

1. Open **Studio Code Server**.
2. Maak in `/config` een map `packages` (als die er nog niet is).
3. Zet daarin het bestand `warmtepomp_thermostaat.yaml` uit de map `packages` van GitHub.
4. Open `configuration.yaml` en zorg dat dit erin staat:

   ```yaml
   homeassistant:
     packages: !include_dir_named packages
   ```

   Staat er al een regel `homeassistant:`, zet dan alleen de regel `packages:` eronder, ingesprongen met twee spaties.

5. **Ontwikkelaarshulpmiddelen > YAML > Configuratie controleren.** Bij "Configuratie in orde": **Opnieuw opstarten** (helemaal, niet alleen herladen).

Daarna bestaan er zes nieuwe entiteiten:

| Entiteit | Wat |
| --- | --- |
| `climate.woonkamer` | De thermostaat |
| `sensor.woonkamer_ha_vraagt_nu` | HA vraagt nu, met de reden als attribuut |
| `input_select.woonkamer_stand` | Automatisch, Handmatig, Koelen, Vakantie |
| `input_number.woonkamer_handmatig` | De vaste temperatuur in de stand Handmatig |
| `input_boolean.woonkamer_instellingen_tonen` | Instellingen op het dashboard tonen |
| `input_boolean.woonkamer_thermostaat_hulp` | Hulpschakelaar van de thermostaat, niet gebruiken |

Heet de thermostaat anders (bijvoorbeeld `climate.woonkamer_2`), hernoem hem dan in de instellingen van de entiteit naar `climate.woonkamer`.

## 2. De blueprint

1. Zet `warmtepomp_thermostaat.yaml` in `blueprints/automation/warmtepomp/` op GitHub.
2. In Home Assistant: **Instellingen > Automatiseringen en scènes > Blueprints > Blueprint importeren**, plak de GitHub-link van het bestand.
3. Maak er een automatisering van. Alle keuzes staan al goed; controleer ze en sla op als **Warmtepomp thermostaat**.

## 3. Het dashboard

Open het tabblad of het dashboard, potlood, drie puntjes, **Raw-configuratie-editor**, vervang alles door de nieuwe `warmtepomp_tabblad.yaml` of `warmtepomp_dashboard.yaml` en sla op.

## 4. Controleren

Werk ook de blueprint **Warmtepomp: woonkamer** bij (opnieuw importeren of het bestand vervangen): die kent nu de stand Handmatig. De bestaande automatisering hoef je niet aan te passen.

| Test | Goed als |
| --- | --- |
| Stand Automatisch | De knop toont hetzelfde als HA vraagt nu |
| Draai de knop naar 20 | De stand springt naar Handmatig; binnen een minuut wordt HA vraagt nu 20, met reden "handmatig" |
| Stand terug op Automatisch | De knop springt naar wat het schema vraagt |
| Stand Vakantie | De schakelaar Vakantie van de controller gaat aan; de knop toont de vakantietemperatuur |
| Zet Vakantie aan op de controller-pagina | De stand springt vanzelf op Vakantie |

## Goed om te weten

- **Koelen** zet de schakelaar Koelvraag van de controller aan. Verwarmen stopt dan meteen. De UVR koelt nog niet: dat wordt later ingericht in TAPPS2, met bewaking van het dauwpunt. Kies Koelen dus nog niet in de winter.
- **"Verwarmen" of "Inactief"** onder het getal in de thermostaat zegt alleen of de kamer onder de comforttemperatuur is. Of de warmtepomp echt draait, zie je bij Compressor in het blok Nu.
- De thermostaat kan niet uit: zet iemand hem op Uit, dan zet de automatisering hem terug.
- Na een herstart, of als je automatiseringen herlaadt, zet de automatisering de knop vanzelf goed.
- Draaien via Google Home telt als draaien aan de knop: de stand gaat dan naar Handmatig.
