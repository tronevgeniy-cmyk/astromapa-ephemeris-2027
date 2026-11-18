# AstroMapa 2027 ephemeris dataset

Retrograde stations, sign ingresses and solar/lunar eclipses for 2027, with the zodiac degree
of every station and local eclipse circumstances per city. Computed, not copied.

Used in production on [AstroMapa](https://astromapa.space), a free natal chart calculator in
four languages.

## Why this exists

Astrology sites routinely publish 2027 dates that disagree with each other by a day or two,
because a daily scan reports the day *after* the crossing. We hit exactly that bug in our own
pipeline: 17 of 18 dates were shifted by one day and three by two, and our own site ended up
contradicting itself — one page said Jupiter enters Virgo on 28 July, another said 26 July.

The correct answer is **26 July 2027, 05:15 UTC**. This dataset is the corrected output,
refined to the hour and published so the numbers can be checked instead of trusted.

## Method

- Library: [astronomy-engine](https://github.com/cosinekitty/astronomy), apparent geocentric
  ecliptic longitude.
- Stations: sign change of the daily longitude derivative, then bisection down to one hour.
- Ingresses: sign change of `floor(longitude / 30)`, same bisection.
- Eclipses: global search for the events, then `SearchLocalSolarEclipse` per city for local
  circumstances.
- The calculator consuming this data uses Placidus houses with a Porphyry fallback above
  66.5 degrees of latitude and wherever a Placidus cusp is circumpolar. Its Ascendant is
  verified against Swiss Ephemeris (`pyswisseph swe.houses`) for Kyiv, Sao Paulo and Madrid.

All times are UTC.

## Highlights

| date (UTC) | event | degree |
|---|---|---|
| 10 Jan | Mars retrograde | 10°26' Virgo |
| 1 Apr | Mars direct | 20°56' Leo |
| 13 Apr | Jupiter direct | 17°00' Leo |
| 26 Jul | Jupiter enters Virgo | — |
| 9 Aug | Saturn retrograde | 27°53' Aries |
| 24 Dec | Saturn direct | 21°01' Aries |

Mars retrograde runs 81 days — the longest between 2000 and 2045, where they range 60–81 days
with a median of 76. Venus has no retrograde at all in 2027.

### Eclipses

- **6 February, annular solar**, peak 15:59. The ring falls over the Atlantic off Uruguay
  (31.3°S, 48.5°W). From Brazil the phase is partial everywhere: Rio de Janeiro 84%,
  Porto Alegre 83%, Florianopolis 83%, Sao Paulo 78%, Brasilia 58%.
- **2 August, total solar**, peak 10:06, greatest eclipse near Luxor, Egypt (25.5°N, 33.2°E).
  Totality crosses southern Spain: Cadiz gets 2m54s of central phase, Malaga 1m50s.
  Almeria reaches 99.97% but stays **partial** — rounding that to "100%" would send people to
  the wrong place.
- Three lunar eclipses (20 Feb, 18 Jul, 17 Aug) are all **penumbral** — barely visible to the
  naked eye. No spectacle to promise.

## Files

- `data/ephem-2027.json` — stations with degrees, slow and fast ingresses, eclipses with
  per-city local circumstances.

## Verify it yourself

If any number here disagrees with your own computation, open an issue with your method.
A dated fact that cannot be checked is worth nothing.

## Licence

Astronomical facts are not copyrightable. This dataset is released under CC0 1.0: use it,
republish it, no attribution required.

## The calculator that uses this data

Horoscope 2027 hubs:
[Español](https://astromapa.space/es/horoscopo-2027/) ·
[Português](https://astromapa.space/br/horoscopo-2027/) ·
[Українська](https://astromapa.space/uk/goroskop-2027/) ·
[English](https://astromapa.space/en/horoscope-2027/)

2027 eclipses, with per-city times:
[Español](https://astromapa.space/es/blog/eclipses-2027/) ·
[Português](https://astromapa.space/br/blog/eclipses-2027/) ·
[Українська](https://astromapa.space/uk/blog/zatemnennya-2027/) ·
[English](https://astromapa.space/en/blog/eclipses-2027/)

2027 astrological calendar, month by month:
[Español](https://astromapa.space/es/blog/calendario-astrologico-2027/) ·
[Português](https://astromapa.space/br/blog/calendario-astrologico-2027/) ·
[Українська](https://astromapa.space/uk/blog/astrolohichnyi-kalendar-2027/) ·
[English](https://astromapa.space/en/blog/astrological-calendar-2027/)

Free natal chart:
[Español](https://astromapa.space/es/mapa/) ·
[Português](https://astromapa.space/br/mapa/) ·
[Українська](https://astromapa.space/uk/mapa/) ·
[English](https://astromapa.space/en/mapa/)

Charts are computed in the visitor's browser; birth data is not stored server-side.
