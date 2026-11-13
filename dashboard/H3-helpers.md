# H3: drie helpers voor het dashboard

Maak ze via **Instellingen > Apparaten en diensten > Helpers > Helper maken**. Gebruik precies deze namen, dan kloppen de entiteiten in het dashboard.

Let op: de regel "Deze helper heet daarna" onder elke helper hoef je nergens in te vullen. Zo heet de helper vanzelf als je hem opslaat.

## 1. Compressor warmtepomp

Kies **Template** en dan **Template-binaire sensor**.

| Veld | Waarde |
| --- | --- |
| Naam | `Compressor warmtepomp` |
| Statustemplate | `{{ states('sensor.energymeter_warmtepomp_power') \| float(0) > 1000 }}` |
| Apparaatklasse | Draaiend (Running) |
| Apparaat | leeg laten |

Deze helper heet daarna: `binary_sensor.compressor_warmtepomp`.

Grens 1.000 W: stilstaand gebruikt de warmtepomp onder 250 W, draaiend boven 1.750 W.

## 2. Starts warmtepomp vandaag

Kies **Historische statistieken** (History stats). Dit gaat in drie schermen.

| Scherm | Veld | Waarde |
| --- | --- | --- |
| 1 | Naam | `Starts warmtepomp vandaag` |
| 1 | Entity (de bron) | **Compressor warmtepomp** |
| 1 | Type | Aantal (Count) |
| 2 | State | **Running** (is hetzelfde als `on`) |
| 3 | Start | `{{ today_at() }}` |
| 3 | End | `{{ now() }}` |
| 3 | Duration | leeg laten |
| 3 | State class | Total increasing |

Deze helper heet daarna: `sensor.starts_warmtepomp_vandaag`.

## 3. Draaitijd warmtepomp vandaag

Weer **Historische statistieken**. Ook hier is de bron de **compressor**, niet de starts.

| Scherm | Veld | Waarde |
| --- | --- | --- |
| 1 | Naam | `Draaitijd warmtepomp vandaag` |
| 1 | Entity (de bron) | **Compressor warmtepomp** |
| 1 | Type | Tijd (Time) |
| 2 | State | **Running** |
| 3 | Start | `{{ today_at() }}` |
| 3 | End | `{{ now() }}` |
| 3 | Duration | leeg laten |
| 3 | State class | Total increasing |

Deze helper heet daarna: `sensor.draaitijd_warmtepomp_vandaag`.

De tellers beginnen bij het aanmaken. De grafiek "Starts per dag" vult zich in de loop van de week.
