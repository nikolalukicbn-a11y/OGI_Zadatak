# Zadatak 5 — EV punjači duž autoputa A-1

**Cilj:** Postaviti brze EV punjače duž autoputa A-1 koristeći greedy algoritam na stacionaži.

## Podaci

| Fajl | Opis |
|---|---|
| `autoput.geojson` | Autoput A-1 (1 LineString, ~306 km) |
| `pumpe.geojson` | 22 benzinske pumpe duž autoputa (kandidati za punjače) |
| `zadatak.md` | Postavka zadatka i uputstvo |

## Rezultati

### Greedy "poslednji u dometu" (optimalna strategija)

| D_max | Broj punjača | Max gap |
|---|---|---|
| 50 km | **7** | 49.6 km |
| 30 km | **12** | 29.1 km |

### Poređenje strategija (D_max = 50 km)

| Strategija | Broj punjača |
|---|---|
| Poslednji u dometu | **7** (optimalno) |
| Prvi u dometu | 21 (lošije) |

> Strategija "poslednji u dometu" postavlja punjač što dalje unutar dozvoljenog dometa, čime maksimizira pokrivenost jednim punjačem i minimizira ukupan broj potrebnih punjača.

### GAP upozorenje

Na km 296.0 postoji GAP — nema benzinske pumpe u dometu od 50 km do kraja autoputa, što znači da poslednji deo autoputa nije pokriven.

## Algoritam

1. Projektovanje svake pumpe na autoput (`linestring.project(point)`) → stacionaža
2. Sortiranje pumpi po stacionaži
3. Greedy skeniranje: u svakom koraku biraj **poslednju** (najdalju) pumpu unutar `D_max`

## Pokretanje

```bash
uv sync
uv run jupyter notebook resenja/Z5_ev_punjaci.ipynb
```

## Tehnologije

- Python 3.13+
- GeoPandas, NumPy, Matplotlib
- Jupyter Notebook
- Upravljanje paketima: `uv`
