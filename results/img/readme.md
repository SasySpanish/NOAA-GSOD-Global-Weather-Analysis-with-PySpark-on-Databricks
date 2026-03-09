## Results and Visualizations

All plots were generated using Seaborn and Matplotlib within PySpark notebooks.  
The images are saved in the `results/img/` folder of this repository. Below is a description of each visualization together with the main insights from the NOAA GSOD data (2014–2024, 77 selected stations).

### 1. Heatmap: Average Days with Precipitation >10 mm per Continent and Year

Shows the **average number of days per year with rainfall >10 mm** across continents.

Europe (EU) stands out with consistently high values (often 30–54 days), peaking in 2016.  
South America (SA) also shows several very wet years (e.g. 2021).  
Asia (AS) and Africa (AF) display moderate but rising trends toward 2024.  
Oceania (OC) remains the driest and most variable, frequently below 5 days in recent years.

![Heatmap: Giorni medi >10mm per Continente e Anno](C.%20giorni%20di%20pioggia%2010mm%20continente%20x%20anno.png) 

### 2. Top 6 Continents by Average Temperature in 2024

Bar chart ranking continents by **mean annual temperature in 2024**.

Africa (AF) is clearly the warmest (~21–22 °C), followed by Asia (AS).  
Europe (EU) ranks last among the six (~14 °C), consistent with its more temperate latitude.

![Top 6 Continenti per Temperatura Media 2024](C.%20temp%20media%20x%20continente%202024.png)

### 3. Heatmap: Temperature Variability (Standard Deviation) per Continent and Year (2014–2024)

Illustrates **intra-annual temperature variability** (standard deviation of daily temperatures).

Asia (AS) and North America (NA) show the highest variability year after year (~5.5–6.3 °C).  
South America (SA) exhibits the lowest and most stable values (~2.5–3.0 °C).  
No strong long-term trend in variability is visible over the decade.

![Heatmap Variabilità Temperatura per Continente e Anno](C.%20heatmap%20variabilità%20temperatura%20continente%2014-24.png)

### 4. Top 10 Cities by Average Temperature in 2024

Horizontal bars ranking **countries** by mean temperature in 2024 (based on selected stations).

Egypt leads (~26 °C), followed by Morocco and others.  
The list includes countries from multiple continents, with a strong presence of warm African and subtropical locations.

![Top10 Paesi per Temp Media 2024](top%2010%20città%20temp%20media%2024.png)

### 5. Top 10 Hottest Cities in 2024

Bar chart of the **10 cities** with the highest annual mean temperature in 2024.

Yola (Nigeria) tops the ranking at ~30 °C, followed by other tropical cities (Nigeria, India, Indonesia, Jamaica, Egypt, etc.).  
Tropical and subtropical stations clearly dominate the hottest positions.

![Top 10 Città Più Calde 2024](top10%20città%20più%20calde%202024.png)

### 6. Boxplot: Average Diurnal Temperature Range (Tmax – Tmin) per Country – Last 5 Years

Boxplot showing **daily temperature range** (maximum – minimum) averaged over the most recent 5 years.

Asia and North America frequently show the largest ranges (40–70 °C in continental locations).  
South America and parts of Africa tend toward smaller ranges (20–40 °C).  
Europe and Oceania are generally more moderate.

![Escursione Termica Media per Paese – Ultimi 5 Anni](P.%20escursione%20termica%20per%20paese%20last5y.png)

### 7. Annual Average Temperature Trend per Continent (2014–2024)

Multi-line chart tracking **mean annual temperature** for each continent over the decade.

Africa shows the highest values (~20–22 °C) with a visible upward tendency in recent years.  
Europe remains the coolest (~14–15 °C) but with slight increases.  
Oceania is the most stable and lowest.  
The plot highlights clear differences in both level and trend among continents.

![Trend Temperatura Media Annuale per Continente 2014–2024](C.%20trend%20temperatura%20annuale%20continente%2014-24.png)

### 8. Top 10 Countries by Average Temperature – Year by Year (2014–2024)

Multi-panel horizontal bar charts (one per year) showing the **top 10 countries** ranked by annual mean temperature each year.

Tropical cities from Nigeria, Jamaica, Indonesia, El Salvador, India, Egypt, Mexico, Brazil and Tanzania repeatedly occupy the top positions.  
Warmest annual averages frequently reach 28–32 °C in the leading cities.  
The pattern is fairly consistent across the decade, with only minor shifts in ranking.

![Top 10 Città per Temperatura Media Annuale – Anno per Anno](P.%20top%2010%20paesi%20per%20temperatura%20media%2014-24.png)

These visualizations together reveal:
- strong tropical influence on the highest temperatures
- higher frequency of heavy rain days in Europe and parts of South America/Asia
- greater temperature variability in Asia and North America
- generally stable or slowly warming continental averages over the 2014–2024 period
