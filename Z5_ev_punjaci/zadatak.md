# Zadatak 5 — EV punjači duž autoputa

**Težina:** ⭐⭐ &nbsp;•&nbsp; **Vreme:** ~60 min

## Postavka

Treba postaviti **brze punjače** duž autoputa **A-1** tako da je **maksimalno
rastojanje između dva uzastopna punjača ≤ 50 km**. Punjač mora biti na **postojećoj
benzinskoj pumpi** (`amenity='fuel'`).

> 🔍 **Trick:** sve se svodi na **stacionažu** — koliko metara od početka autoputa.
> Funkcija `linestring.project(point)` daje stacionažu (1D problem).

## Fajlovi

- `autoput.geojson` — 1 LineString (autoput A-1, ~300 km)
- `pumpe.geojson` — 22 benzinske pumpe duž autoputa (kandidati)

## Algoritam — 1D greedy scan

```python
autoput_line = autoput.geometry.iloc[0]
ukupna_km = autoput_line.length / 1000

# 1) Project svaki kandidat na autoput
pumpe["stacionaza"] = pumpe.geometry.apply(lambda p: autoput_line.project(p))
pumpe = pumpe.sort_values("stacionaza").reset_index(drop=True)

# 2) Greedy: u svakom koraku biraj POSLEDNJU pumpu u dometu (D_max = 50 km)
D_max = 50_000  # m
izabrani = []
prethodno_km = 0
while prethodno_km < autoput_line.length:
    validni = pumpe[
        (pumpe["stacionaza"] > prethodno_km) &
        (pumpe["stacionaza"] <= prethodno_km + D_max)
    ]
    if validni.empty:
        print(f"GAP od km {prethodno_km/1000:.1f} — nema kandidata u dometu od {D_max/1000} km!")
        break
    izbor = validni.iloc[-1]  # poslednja validna = najdalja u dometu
    izabrani.append(izbor)
    prethodno_km = izbor["stacionaza"]

print(f"Postavljeno punjača: {len(izabrani)} na autoputu od {ukupna_km:.0f} km")
```

## Vizualizacija

- Autoput kao **plava debela linija**.
- Sve pumpe kao **sivi krugovi**.
- Izabrani punjači kao **zeleni krugovi** sa labelom km.
- Crvena oznaka tamo gde je razmak između susednih > D_max.

## Pitanja u izveštaju

1. Koliko punjača treba za D_max=50 km? A za D_max=30 km?
2. Postoji li deo autoputa gde **gap** (razmak između susednih pumpi) prelazi 50 km?
3. Da li bi greedy strategija "izaberi prvog u dometu" dala manji broj punjača od "poslednji u dometu"? Probaj.

## Predaja

- `ime_prezime_Z5.ipynb` sa rešenjem i 3 odgovora.
