# E6B Flight Computer

Digitaler Flugcomputer im Browser — ein einzelnes HTML-File, keine Abhängigkeiten, offline nutzbar.

## Funktionen

| Modul | Inhalt |
|---|---|
| **Analog-Rechenschieber** | Drehbare Scheibe wie beim mechanischen E6B: logarithmische A/B-Skalen (eine Dekade pro Umdrehung), Gradring, ziehbar mit Schwung, animiertes Andrehen, Zeiger frei drehbar, Ablesetabelle |
| **Winddreieck** | Steuerkurs (TH), Abtrift (WCA), Grundgeschwindigkeit (GS), Gegen-/Rückenwind, Seitenwind, grafische Vektordarstellung |
| **Kraftstoff & Reichweite** | Flugzeit, Verbrauch, Reserve in Minuten, Reichweite pro Liter, Restmengen-Check |
| **Zeit · Geschwindigkeit · Strecke** | jeweils dritter Wert aus zwei bekannten |
| **Dichtehöhe & IAS→TAS** | ISA-Abweichung, Dichtehöhe, Luftdichte, TAS-Näherung, Startstrecken-Verlust, Druckhöhe aus QNH |

Einheitensystem umschaltbar: **metrisch** (km/h, km, m, L) und **imperial** (kts, nm, ft, US gal).

## Rechengrundlagen

- **Winddreieck** — exakte Vektorlösung: `TAS·sin(TH−TC) + Vw·sin(Δ) = 0`, mit `Δ = Windrichtung_aus + 180° − TC`.
  `GS` ist der Betrag der Vektorsumme. Ein nicht fliegbarer Kurs (Seitenwind > TAS) wird als Fehler gemeldet.
- **Dichtehöhe** — nach ISA: `DA = PA + 118,8 m · (OAT − ISA_T)`, `ρ = ρ₀·(1 − 2,2558·10⁻⁵·DA)^4,2559`.
  Die verbreitete Faustformel „120 ft pro °C" ist **nicht** metrisch anwendbar (≈ 36,6 m pro °C).
- **TAS aus IAS** — `TAS ≈ IAS · √(ρ₀/ρ)`, IAS als CAS genähert.
- **Rechenschieber** — Winkel = `360° · log₁₀(v/10)`. Die Scheibe wird so gedreht, dass der
  Bezugswert 60 der Innenskala unter dem Außenwert liegt; an jeder Strahllinie gilt dann
  `außen = innen · a / b`. Der Dezimalpunkt wird wie beim echten Gerät im Kopf gesetzt —
  die Tabelle darunter liefert die fertigen Werte.

## Nutzung

`e6b.html` im Browser öffnen — fertig. Keine Installation, kein Server, kein Tracking.
Alternativ über GitHub Pages hosten.

## Grenzen

- Näherungen für Flugplanung, **kein Ersatz** für AFM/POH, offizielle Wetterdaten oder zugelassene Flugplanungswerkzeuge.
- Magnetische Missweisung (Variation) und Deviation sind nicht berücksichtigt — Kurse sind echte Kurse (True).
- Temperaturkorrekturen der Höhenmesseranzeige nach ICAO-Standardatmosphäre.

## Lizenz

MIT — siehe [LICENSE](LICENSE).
