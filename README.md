# MUHC Vehicule Routing Optimization

This project tackles **route optimization** for MUHC (healthcare logistics context). The notebook builds data inputs, constructs a travel cost matrix, formulates a routing/optimization model, and produces **optimized routes** with optional visualization.

> Source file: `MUHC Route Optimization.ipynb`

---

## What the notebook does

- Build a distance/time matrix between stops.
- Formulate a Vehicle Routing Problem (VRP) with capacity/time constraints.
- Solve the optimization model (e.g., OR-Tools / PuLP) to generate routes.
- Visualize routes on a map and/or export route summaries.
- Prepare/validate geocoded locations (lat/lon) for all stops and depots.
- (Optional) Enforce time windows for deliveries/visits.
- (Optional) Impose max shift duration, distance, or number of stops per route.

---

## Environment & setup

Use **Python ≥ 3.10** (recommended). Install detected dependencies:
```bash
pip install gurobipy folium matplotlib IPython numpy pandas requests
```

> If your solver requires extras (e.g., `ortools` for CP-SAT, or `pulp` with CBC/Gurobi), ensure they’re installed and on PATH.

---

## Inputs & assumptions

Typical expected inputs:

- **Stops/locations** with at least: `id`, `latitude`, `longitude` (and optionally demand, service time, time windows).
- **Depot / start-end** locations for vehicles.
- **Vehicle parameters**: number of vehicles, capacity (if CVRP), optional max route length/duration.
- **Business rules** (optional): time windows, priority flags, required visit frequencies, etc.

> The notebook will compute or read a **distance/time matrix** to evaluate route costs. If OSM-based methods are used (e.g., `osmnx`), an internet connection may be needed for graph retrieval the first time.

---

## Running the notebook

1. Place your input files next to the notebook (e.g., `.csv` with stops and depot(s)).
2. Open `MUHC Route Optimization.ipynb` and run cells in order.
3. Adjust **parameters** (vehicle count, capacities, max distance/time, time windows) in the configuration cells.
4. Run the **solver** cells to generate routes.
5. Inspect **outputs**:
   - Route assignments per vehicle
   - Total distance/time summaries
   - (Optional) Map plots or GeoDataFrames

---

## Key functions/sections (detected)
Below is a generic checklist matched to typical code blocks you’ll find:
- **Data preparation**: cleaning, deduping locations, geocoding validation.
- **Matrix building**: great-circle (Haversine) or network-based (OSM/OSRM) distances.
- **Model formulation**: decision variables for visit/sequence, flow constraints, capacity/time-window constraints.
- **Solving**: OR-Tools (RoutingModel/CP-SAT) or PuLP (MILP with CBC/Gurobi).
- **Post-processing**: sequence decoding, KPIs, exporting CSV/GeoJSON, plotting.

---

## License & attribution

- Routing/VRP examples often build on **OR-Tools** or **PuLP** models.
- Geographic data may rely on **OpenStreetMap** via `osmnx`/`folium`.
- Ensure compliance with institutional and data-sharing policies (PHI/PII handling if any).
