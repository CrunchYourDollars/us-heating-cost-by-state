# US heating cost by state, 2026-27

Estimated yearly cost to heat the same reference home in all 50 states and DC with five heating systems: natural gas furnace, propane furnace, heating oil boiler, electric resistance and air-source heat pump.

- **Data:** [`heating-cost-by-state-2026-27.csv`](heating-cost-by-state-2026-27.csv) (one US reference row plus 51 state rows; the first three lines are `#` comments)
- **Interactive table and full write-up:** https://crunchyourdollars.com/heating-cost-by-state

These are modeled estimates for one reference home in a normal winter, not measured bills.

## Reference home

2,000 sq ft, average insulation (0.35 BTU/hr per sq ft per F).

## Method

Heat needed (Btu) = floor area x 0.35 x HDD65 x 24 x 0.75, the ASHRAE degree-day method. The 0.75 factor corrects for heat from people, lights and sun.

Fuel bought = heat needed / system efficiency / fuel heat content.

| System | Efficiency | Heat content |
|---|---|---|
| Natural gas furnace | 95% AFUE | 100,000 Btu per therm |
| Propane furnace | 95% AFUE | 91,452 Btu per gallon |
| Heating oil boiler | 85% AFUE | 138,500 Btu per gallon |
| Electric resistance | 100% | 3,412 Btu per kWh |
| Air-source heat pump | 8.1 HSPF2 | kWh = heat needed / (HSPF2 x 1,000) |

HSPF2 is rated for a mid climate. In climate zones 5 to 7 the data uses a lower cold-climate value, about 19% lower; see the `heat_pump_hspf2` column.

## Sources

- **Electricity and natural gas:** EIA residential prices, 2025 annual.
- **Propane and heating oil:** EIA weekly residential survey, averaged over October 2026.
- **Heating degree days:** population-weighted state normals, 1991-2020 (NOAA CPC / NCEI).

## Columns

| Column | Meaning |
|---|---|
| `state`, `code` | State name and postal code |
| `climate_zone` | Climate zone |
| `hdd65_normal_1991_2020` | Heating degree days, base 65 F |
| `heat_needed_mmbtu` | Yearly heat the home needs, million Btu |
| `electricity_cents_per_kwh` | Residential electricity price |
| `natural_gas_usd_per_therm`, `propane_usd_per_gallon`, `heating_oil_usd_per_gallon` | Fuel prices |
| `*_price_level` | `state` = the state's own price, `padd` = EIA regional price, `us` = US average, `state-prior-year` = the state's prior-year annual price |
| `heat_pump_hspf2` | Heat pump efficiency used |
| `cost_*` | Yearly cost in USD by system |
| `cheapest` | Cheapest system for that state |

## Limits

- Oil and propane costs use one month's price. The October 2026 heating oil average was about $6.16 a gallon. EIA's 2026-27 Winter Fuels Outlook expects about $5.26 from November through March, which would lower the US oil figure from $2,788 to $2,381.
- Many states use a regional or US fallback price for oil or propane. Check the `*_price_level` columns before comparing them. Alaska's oil and propane figures, for example, use US average prices.
- Running costs only. Installation and maintenance are not included.
- Real bills depend on the house, the equipment, the thermostat and the weather.

## License and citation

The compiled table and cost estimates are licensed under [CC BY 4.0](LICENSE). Underlying EIA and NOAA data remain subject to their publishers' terms.

Suggested credit: CrunchYourDollars, from EIA prices and NOAA climate normals, with a link to https://crunchyourdollars.com/heating-cost-by-state

## Disclosure

CrunchYourDollars is a small independent home cost site that earns affiliate commissions on home equipment.
