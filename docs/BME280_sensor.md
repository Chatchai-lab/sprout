# Temperatur-, Luftfeuchtigkeits- und Luftdrucksensor (BME280)

## Übersicht & Auswahlbegründung
Der **BME280** dient in unserem automatisierten Mini-Gewächshaus zur kontinuierlichen Erfassung der Umgebungstemperatur, der relativen Luftfeuchtigkeit sowie des Luftdrucks. 

**Warum dieses Bauteil gewählt wurde:**
* **Direkte Stromversorgung:** Der Sensor arbeitet mit $3,3\,\text{V}$ und verbraucht extrem wenig Strom ($< 1\,\text{mA}$). Er kann daher ohne separates Netzteil direkt über den Raspberry Pi versorgt werden.
* **Einfacher Anschluss:** Dank der $\text{I}^2\text{C}$-Schnittstelle werden insgesamt nur vier Leitungen (Stromversorgung + zwei Datenleitungen) benötigt.
* **Präzision & Software-Support:** Der Sensor liefert zuverlässige digitale Messwerte und wird von gängigen Python-Bibliotheken nativ unterstützt.

---

## Bezugsquelle & Dokumentation
* **Bezugsquelle:** [ARCELI BME280 Modul auf Amazon](https://www.amazon.de/ARCELI-Digitaler-Barometrischer-Temperatur-Luftfeuchtigkeit/dp/B0CLS2VQMR)
* **Datenblatt:** `\sprout\docs\Datenblätter\BME280_Sensor Luchtfeuchtigkeit_Temperatur.pdf`

---

## Verkabelung & Pinbelegung ($\text{I}^2\text{C}$)

> **Wichtiger Hardware-Hinweis:** Der Sensor **muss** an den **$3,3\,\text{V}$-Pin** angeschlossen werden. Die Datenleitungen des Raspberry Pi sind nicht $5\,\text{V}$-tolerant – eine Versorgung mit $5\,\text{V}$ kann die GPIOs oder den Prozessor beschädigen.

| BME280 Pin | Raspberry Pi Pin (Board) | Raspberry Pi GPIO (BCM) | Funktion |
| :--- | :--- | :--- | :--- |
| **VCC / VIN** | Pin 1 | $3,3\,\text{V}$ Power | Stromversorgung ($3,3\,\text{V}$) |
| **GND** | Pin 6 | Ground | Gemeinsame Masse |
| **SDA** | Pin 3 | GPIO 2 (SDA) | Bidirektionale Datenleitung |
| **SCL** | Pin 5 | GPIO 3 (SCL) | Taktleitung |

### Die vier verwendeten Pins im Detail
* **Pin 1 ($3,3\,\text{V}$ Power):** Ein reiner Stromversorgungs-Ausgang. Er liefert dauerhaft $3,3\,\text{Volt}$, sobald der Raspberry Pi am Netzteil hängt (lässt sich nicht per Software ausschalten).
* **Pin 6 (GND / Ground):** Der gemeinsame Bezugspunkt (Masse / Minuspol) für den Stromkreis. Alle Komponenten, die miteinander kommunizieren, müssen über GND verbunden sein, damit sie denselben Spannungsbezug haben.
* **Pin 3 (GPIO 2 / SDA – Serial Data):** Über diese bidirektionale Datenleitung sendet der Raspberry Pi Anfragen an den BME280 (z. B. *„Gib mir die aktuelle Temperatur“*) und empfängt im Gegenzug die Messwerte als digitale Einsen und Nullen.
* **Pin 5 (GPIO 3 / SCL – Serial Clock):** Die Taktleitung. Der Raspberry Pi gibt hierüber einen festen Takt vor (meist $100\,\text{kHz}$), damit Sensor und Pi genau wissen, wann ein einzelnes Datenbit auf der SDA-Leitung gültig ist.

---

## Software & Auswertung (Python)
Für die Auswertung der Rohdaten ist keine manuelle Bit-Verarbeitung notwendig. Auf dem Raspberry Pi muss lediglich die $\text{I}^2\text{C}$-Schnittstelle aktiviert werden (`raspi-config`). 

In Python übernimmt eine fertige Bibliothek (z. B. `adafruit-circuitpython-bme280` oder `RPi.bme280`) die Kommunikation über die $\text{I}^2\text{C}$-Adresse (`0x76` oder `0x77`) und gibt direkt fertige Messwerte aus (z. B. `23.4 °C` und `68.2 %`).

---

## Mechanische Integration (Hinweise für den Aufbau)
* **Schutz vor Feuchtigkeit:** Die Platine des Sensors darf nicht direkt vom Sprühwasser der Bewässerung getroffen werden und es sollte kein Kondenswasser auf die Kontakte tropfen. Ein kleines, nach unten offenes Schutzdach (ähnlich einer Wetterstation) sorgt für ausreichende Luftzirkulation bei gleichzeitigem Spritzwasserschutz.
* **Kabellänge:** Bei größeren Abständen zwischen Raspberry Pi (Elektronikfach) und Messpunkt im Pflanzenraum empfiehlt sich ein vieradriges, geschirmtes Kabel, um Störungen auf der $\text{I}^2\text{C}$-Leitung zu vermeiden.