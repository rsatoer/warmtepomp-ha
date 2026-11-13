# H5: helpers voor de woonkamer

Maak ze via **Instellingen > Apparaten en diensten > Helpers > Helper maken**. Gebruik precies deze namen, dan vindt de blueprint "Warmtepomp: woonkamer" ze vanzelf.

## 1. Weekschema

Kies **Schema**.

| Veld | Waarde |
| --- | --- |
| Naam | `Warmtepomp comfort` |
| Uren | Teken per dag de uren waarin het comfortabel warm moet zijn. |

Deze helper heet daarna: `schedule.warmtepomp_comfort`.

## 2. Vier temperaturen

Kies vier keer **Getal** (Number). Bij elk getal: Weergavemodus **Schuifregelaar**, Stapgrootte **0.5**, Eenheid **°C**.

| Naam | Minimum | Maximum | Zet daarna op | Deze helper heet daarna |
| --- | --- | --- | --- | --- |
| `Woonkamer comfort` | 15 | 25 | 19 | `input_number.woonkamer_comfort` |
| `Woonkamer laag` | 15 | 25 | 17 | `input_number.woonkamer_laag` |
| `Woonkamer toeslag thuis` | 0 | 3 | 1 | `input_number.woonkamer_toeslag_thuis` |
| `Woonkamer vakantie` | 15 | 25 | 16 | `input_number.woonkamer_vakantie` |

Een nieuw getal begint op het minimum. Zet het daarna op de waarde uit de kolom "Zet daarna op", met de schuif op het dashboard of in de helper zelf.

De regel "Deze helper heet daarna" hoef je nergens in te vullen. Zo heet de helper vanzelf als je hem opslaat.
