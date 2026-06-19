# OGI Zadatak 5 — EV punjaci duz autoputa A-1

**Predmet:** Osnove geoprostorne inteligencije (OGI)
**Autor:** Nikola Lukic, Dusan Kozomara, Marija Blagojevic, Marko Pecanac

## Opis projekta

Postavljanje brzih EV punjaca duz autoputa A-1 (~306 km) koristeci greedy algoritam na stacionazi. Punjači se postavljaju samo na postojecim benzinskim pumpama.

## Struktura

```
OGI_Zadatak/
  Z5_ev_punjaci.ipynb      # Resenje (Jupyter notebook)
  Z5_ev_punjaci/
    autoput.geojson        # Autoput A-1 (LineString)
    pumpe.geojson          # 22 benzinske pumpe (kandidati za punjace)
    zadatak.md             # Postavka zadatka
    README.md              # Detaljni opis zadatka
```

## Rezultati

| D_max | Broj punjaca | Max gap |
|-------|-------------|---------|
| 50 km | 7           | 49.6 km |
| 30 km | 12          | 29.1 km |

Strategija "poslednji u dometu" daje 7 punjaca (optimalno), dok "prvi u dometu" daje 21.

## Pokretanje

```bash
uv sync
uv run jupyter notebook Z5_ev_punjaci.ipynb
```

## Tehnologije

- Python 3.13+ (GeoPandas, NumPy, Matplotlib)
- Jupyter Notebook
- `uv` za upravljanje paketima
