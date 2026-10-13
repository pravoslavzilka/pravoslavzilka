# Pravoslav Žilka

Final-year mechanical engineering undergraduate at Brno University of Technology.
I build instrumented physical systems and the software that runs them — field sensor
hardware, firmware on a power budget, and dynamic system models calibrated against
real plant data.

Currently modelling a cryogenic helium cooling loop at the Institute of Plasma
Physics in Prague. Applying for PhD entry in autumn 2027, in sensing, mechatronics
and thermal-fluid systems.

---

### DryAhead — soil-moisture sensor network for drought risk
**[pravoslavzilka/DryAhead](https://github.com/pravoslavzilka/DryAhead)** · solo · live at dryahead.com

Five LoRa nodes and a hub running unattended since June 2026 across a 500 m radius in
central Slovakia. 42,003 readings at day 105. Delivery is 80–87% on the nodes in
service; the aggregate 58% reflects one node dead for most of the period and one
retired, so the ceiling sits on enclosure reliability rather than the radio link or
the cloud stack.

- ESP32 + SX127x at 433 MHz, DS3231 RTC waking the board, capacitive probe,
  peripheral power gating, 11–12 µA deep sleep, 14 days of local retention
- RSSI held at −95 to −97 dBm with no distance dependence inside 1 km
- Reconciliation over a `GETDATA` pull; one tested 59.6 h outage recovered only 23%,
  because reconciliation ran after the retention window had rolled
- Supabase/PostgreSQL, React dashboard on Vercel

**On the model.** The first version — a combined FAO-56 root-zone bucket with nine free
parameters, calibrated by differential evolution — lost to a persistence baseline at
every horizon on every node. A synthetic two-year run recovered the parameters
cleanly, which pointed at identifiability rather than wrong physics, so I split it
into separate drying and wetting models of five parameters each, fitted per node
against a local weather station. Held-out 7-day RMSE in raw counts:

| Node | Drying model | Persistence | Average drift |
|---|---|---|---|
| 1 | **9.5** | 14.9 | 26.6 |
| 4 | **8.6** | 59.4 | 69.5 |
| 5 | **8.0** | 47.5 | 20.7 |

The original combined model is kept as a baseline and still loses. Results are
indicative — 5–9 forecasts per node — and the fit is on summer data only, so autumn
and winter are extrapolation. Sensors are not yet calibrated against a gravimetric
reference, so readings are a relative signal rather than volumetric moisture.

### iGEM Brno 2025 — duckweed cultivator
**[2025.igem.wiki/brno-czech-republic/hardware](https://2025.igem.wiki/brno-czech-republic/hardware)**

Hardware lead on a fully functional duckweed cultivator that produced experimental
data and was, in the team's view, a main reason we won. I owned the overall concept
and designed the dosing system, the reservoir section, the flushing system and the
PROBE assembly, along with almost all of the printed parts.

Other groups working on non-duckweed systems approached us to consult on their own
cultivator designs, and we received offers to build further units. I also wrote most
of the team wiki, entered the cultivator into the Booster Challenge — the prize money
part-funded the team — coordinated workshop access for the build, handled university
liaison, and arranged transport of the machine to Paris.

### COMPASS-U cryogenic cooling loop — Institute of Plasma Physics, Prague
**[pravoslavzilka/compass-u-cryo-loop](https://github.com/pravoslavzilka/compass-u-cryo-loop)**

Dynamic thermal-hydraulic model of the cryogenic helium loop cooling the COMPASS-U
tokamak's poloidal field coils. Modelica in Dymola with the TIL library, split-range
inventory control, parameters fitted by differential evolution against plant data,
scored by KGE with held-out validation.

### NitroCat — enzyme discovery for a target reaction
**[nitroduckmafia](https://github.com/nitroduckmafia)** · wound down, kept as a record

A pipeline that takes a desired chemical reaction and returns ranked enzyme
candidates. My main contribution was **CoBaCo** (Constraint Batch Construction), a
training modification to CLIPZyme's contrastive enzyme–reaction objective: batches are
built from distinct EC4 classes so same-EC4 enzymes never co-occur and register as
false negatives, with inverse-frequency sampling within a class so common enzymes
don't dominate.

Also built the FastAPI screening service (CLIPZyme ranking, UniProt/SABIO-RK/BRENDA
enrichment, Rhea similarity search, deployed on Railway) and an offline harness
benchmarking it against CLAIRE across a 67-run sweep over margin, schedule and EC
level.

---

**Tools** — C++/Arduino and PlatformIO on ESP32 · Python, FastAPI, scikit-learn ·
Modelica in Dymola and OpenModelica · React · PostgreSQL · Fusion 360 and FDM printing

**Reach me** — macky_na_mori@proton.me
