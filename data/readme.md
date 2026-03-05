## Data - Cities, Weather Stations & Processed Dataset Documentation

This folder contains metadata and documentation related to the weather stations and the final processed dataset used in the analysis.

**No raw CSV files** from NOAA are stored here (they would be >1–2 GB and are not version-controlled).  
Instead, we provide:

- station selection metadata
- documentation of the processing steps
- description of the final schema

## Selected weather stations (77 total)

The analysis uses **77 representative stations** carefully chosen to cover major population centres and different climate zones across all continents.

```text
Europa (Europe)
• Italia:       Bolzano, Roma Ciampino, Palermo Punta Rasi           (3)
• Francia:      Paris CDG, Marseille, Brest                         (3)
• Germania:     Berlin, München, Hamburg                            (3)
• Spagna:       Madrid Barajas, Barcelona, Málaga                   (3)
• Regno Unito:  London Heathrow, Birmingham, Aberdeen               (3)

Asia
• Cina:         Beijing, Shanghai, Guangzhou                        (3)
• India:        Delhi, Mumbai, Chennai                              (3)
• Giappone:     Tokyo, Osaka, Naha Okinawa                          (3)
• Russia:       Moscow, Novosibirsk, Sochi                          (3)
• Indonesia:    Jakarta, Surabaya, Denpasar Bali                    (3)

Africa
• Sudafrica:    Cape Town, Johannesburg, Durban                     (3)
• Nigeria:      Lagos, Kano, Abuja                                  (3)
• Egitto:       Cairo, Alexandria, Aswan                            (3)
• Kenya:        Nairobi, Mombasa, Eldoret                           (3)
• Marocco:      Casablanca, Marrakech, Tanger                       (3)

Nord America
• Stati Uniti:  New York JFK, Los Angeles, Miami                    (3)
• Canada:       Toronto, Vancouver, Montreal                        (3)
• Messico:      Mexico City, Monterrey, Cancún                      (3)
• Cuba:         Havana, Santiago de Cuba                            (2)
• Guatemala:    Guatemala City                                      (1)

Sud America
• Brasile:      Rio de Janeiro, São Paulo, Manaus                   (3)
• Argentina:    Buenos Aires, Córdoba, Ushuaia                      (3)
• Cile:         Santiago, Punta Arenas                              (2)
• Colombia:     Bogotá, Cartagena                                   (2)
• Perù:         Lima, Cusco                                         (2)

Oceania
• Australia:    Sydney, Melbourne, Perth, Darwin, Adelaide          (5)
• Nuova Zelanda: Auckland, Christchurch, Wellington                 (3)
```
- Total: 77 stations × 25 years (2000–2024) = 1,925 CSV files originally read from S3.
- Full station metadata (including exact names, coordinates, elevation, etc.) can be found in the official NOAA file: `isd-history.txt` → https://www.ncei.noaa.gov/pub/data/noaa/isd-history.txt
## Data Processing Summary

All **1,925 CSV files** were read directly from the public Amazon S3 bucket  
`s3a://noaa-gsod-pds/YYYY/USAF99999.csv`  
(no cost, no registration required).

### Main transformations applied

- Temperature conversion: °F → °C (`TEMP_c`, `MAX_c`, `MIN_c`)
- Added derived columns:
  - `year` (extracted from DATE)
  - `season` (Winter / Spring / Summer / Autumn – meteorological definition: Dec–Feb, Mar–May, Jun–Aug, Sep–Nov)
  - `city` (cleaned short name, e.g. "ROMA CIAMPINO" → "Roma Ciampino")
  - `region` (Nord / Centro / Sud – approximate classification based on latitude; mostly meaningful for European/Italian stations)

- Filtered out completely invalid rows (missing temperature)

## Delta Lake
- Final data saved as **Delta Lake table** inside a Databricks **Volume**  
  → avoids re-downloading and re-processing the entire dataset every time

**Approximate final size**: ~690,000 daily records (after light cleaning)

## Variables in the Delta table

| Column              | Type     | Description / Unit                                                                 |
|---------------------|----------|-------------------------------------------------------------------------------------|
| STATION             | long     | NOAA station identifier (original)                                                 |
| DATE                | date     | Observation date (YYYY-MM-DD)                                                      |
| LATITUDE            | double   | Station latitude (°N positive)                                                     |
| LONGITUDE           | double   | Station longitude (°E positive)                                                    |
| ELEVATION           | double   | Station elevation above sea level (meters)                                         |
| TEMP                | double   | Mean temperature – **original °F** (kept for reference)                            |
| TEMP_c              | double   | Mean temperature – **converted °C**                                                |
| MAX                 | double   | Maximum temperature (°F – original)                                                |
| MAX_c               | double   | Maximum temperature (°C)                                                           |
| MIN                 | double   | Minimum temperature (°F – original)                                                |
| MIN_c               | double   | Minimum temperature (°C)                                                           |
| DEWP                | double   | Mean dew point temperature (°F – original)                                         |
| SLP                 | double   | Mean sea level pressure (hPa / mb)                                                 |
| STP                 | double   | Mean station pressure (hPa / mb)                                                   |
| VISIB               | double   | Mean visibility (miles)                                                            |
| WDSP                | double   | Mean wind speed (knots)                                                            |
| MXSPD               | double   | Maximum sustained wind speed (knots)                                               |
| GUST                | double   | Maximum wind gust (knots)                                                          |
| PRCP                | double   | Precipitation amount (**inches** – original NOAA unit)                             |
| SNDP                | double   | Snow depth (inches)                                                                |
| FRSHTT              | integer  | Flags for Fog, Rain, Snow, Hail, Thunder, Tornado (6-digit binary string)          |
| USAF                | string   | 6-digit USAF station code (used to match stations)                                 |
| year                | integer  | Extracted year                                                                     |
| season              | string   | Meteorological season: Inverno, Primavera, Estate, Autunno                         |
| city                | string   | Cleaned city / airport name                                                        |
| region              | string   | Approximate geographic region (mainly Nord/Centro/Sud – latitude-based)           |
| TEMP_ATTRIBUTES     | double   | Attribute flags for TEMP (number of observations, source, etc.)                   |
| DEWP_ATTRIBUTES     | double   | Attribute flags for DEWP                                                           |
| ..._ATTRIBUTES      | *        | All other attribute columns follow NOAA GSOD standard                              |

**Note on precipitation**  
Precipitation is kept in **inches** (original NOAA GSOD unit).  
To convert to millimeters: multiply by **25.4** in queries or visualizations.
Note: precipitation is kept in inches (original NOAA GSOD unit).
If mm are preferred, multiply by 25.4 in queries/visualizations.
