# Googlemaps Triangulate

**Constraint-based restaurant discovery using the Google Maps Platform and geospatial filtering.**

> **Source Available** — This repository is published for portfolio review and educational reference only. See [LICENSE](LICENSE) for terms.

---

## Overview

Finds restaurants that satisfy simultaneous travel-time and quality constraints from two origin points in New York City. Given two addresses, the system filters a curated restaurant database to surface only venues reachable by subway within a specified time budget from **both** locations, ranked by Google rating.

Built to solve a real coordination problem: choosing a meeting-point restaurant that is fair and convenient for two people traveling from different parts of the city.

## Technical Architecture

### Data Pipeline
1. **Address Validation** — Geocodes every restaurant address via the Google Maps Geocoding API; handles multi-location entries by expanding them through the Places API
2. **Quality Filter** — Queries Google Place Details for current ratings; eliminates venues below a configurable threshold (default: 4.5 stars)
3. **Travel-Time Computation** — Calculates subway transit duration from both origins using the Google Maps Directions API with arrival-time predictions
4. **Constraint Satisfaction** — Returns only restaurants where both travel times fall within the time budget (default: 45 minutes)

### APIs & Services
| API | Purpose |
|---|---|
| Geocoding API | Address → coordinates |
| Places API | Venue search and detail retrieval |
| Directions API | Subway transit-time calculations |
| Distance Matrix API | Batch distance/duration queries |

### Stack
- **Google Maps Platform** — Geocoding, Places, Directions, Distance Matrix
- **pandas** — Data manipulation and filtering
- **Python** — Core logic and API orchestration

## Data

- `japanese_restaurants.csv` — Raw restaurant list (name, address)
- `cleaned_japanese_restaurants.csv` — Validated dataset with geocoded addresses

## Results

The system reliably surfaces 4.5+ star restaurants reachable within 45 minutes by subway from both Astoria and Brooklyn starting points, reducing a manual search problem from hundreds of candidates to a ranked shortlist.

## Legal Notice

Copyright (c) 2024-2026 Clarence Stephen. All rights reserved.

This repository is **source available**, not open source. Viewing is permitted for educational and portfolio review purposes. Commercial use, redistribution, and derivative works are prohibited without written authorization. See [LICENSE](LICENSE) for full terms.
