<img width="742" height="474" alt="MyProfile_2" src="https://github.com/user-attachments/assets/cb81174a-41a9-4cd0-b239-d2bb9f2d2152" />
<img width="1911" height="647" alt="MyProfile_1" src="https://github.com/user-attachments/assets/57f3bd11-7cf2-4a84-a3b8-b4ca54cd6b9d" />
# MyProfile / MyProfile1 – Custom Volume Profile (NinjaTrader 8)

A set of two custom Volume Profile indicators developed in 2022 for NinjaTrader 8, focused on performance optimization and session-aware rendering.

---

## Motivation

Existing Volume Profile implementations were too slow for real-time trading workflows with large historical datasets.

This implementation focuses on:

- reducing unnecessary recalculation
- rendering only visible chart regions
- session-aware volume aggregation
- support for intraday and daily structures

---

## Indicators

### MyProfile (Intraday Multi-Timeframe Profile)

Designed for intraday trading and multi-timeframe analysis.

Key characteristics:
- Uses secondary data series (minutes or hours)
- Profile timeframe must be greater than chart timeframe
- Supports 30s–5m charts with higher timeframe aggregation
- Configurable profile resolution
- Session-aware segmentation

Use case:
- intraday structure analysis
- short-term volume clusters
- scalping / intraday context

---

### MyProfile1 (Daily Session Profile)

Designed for higher timeframe and daily structure analysis.

Key characteristics:
- Session-based aggregation using SessionIterator
- One profile per trading day
- 120-minute chart optimized usage
- Simplified data model without secondary series

Use case:
- daily volume distribution
- institutional level structure
- swing context

---

## Core Optimization Idea

Both indicators implement a performance optimization strategy:

> Only profiles visible in the current chart viewport are rendered and processed.

Instead of recomputing full historical profiles, the rendering engine:

- identifies visible sessions
- selects only relevant profile dictionaries
- skips off-screen computation

This significantly reduces rendering overhead on large datasets.

---

## Data Model

- Volume stored per price level (tick aggregation)
- Session segmented dictionaries:
  Dictionary<double, VolumeInfoItem>
- List-based session history:
  List<Dictionary<double, VolumeInfoItem>>

---

## Limitations

- No automatic memory pruning for historical sessions
- Rendering is CPU-bound in OnRender
- Brushes are recreated per render cycle (performance cost)
- Designed for personal / research use, not production-grade distribution

---

## Notes

- Built in 2022
- Based on modified NinjaTrader VolumeProfile implementation
- Optimized for speed rather than feature completeness
