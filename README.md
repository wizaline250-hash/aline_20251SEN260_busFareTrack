# BusFareTrack: Public Bus Trip and Fare/Revenue Monitor

**Student:** Uwimana Aline
**ID:** 20251SEN260
**Course:** INSY 8311 Database Development with PL/SQL (AUCA)
**Instructor:** Eric Maniraguha
**Repository:** `aline_20251SEN260_busFareTrack`

## Problem statement
Public bus operators collect fares from many buses, routes and trips every day. When fare records are scattered or checked by hand, money goes missing without anyone noticing and managers cannot see how much was actually collected. Reports on Kigali's bus reform describe this: old fare collection caused revenue leakage and limited visibility of collected money. BusFareTrack is an Oracle database that records every trip and fare transaction, calculates revenue per route and bus, and flags unusual revenue automatically.

## Objectives
**Main objective:** Build an Oracle PL/SQL database that monitors public bus trips and fare revenue and helps detect revenue leakage.

**Specific objectives**
1. Design a 3NF schema for operators, routes, vehicles, trips and fare transactions.
2. Load and validate a real public dataset of bus fare validations.
3. Use PL/SQL procedures, functions, cursors and packages to record fares and calculate daily revenue.
4. Use triggers and an audit log to block invalid or altered fare records and keep a trace of every change.
5. Provide an Oracle APEX dashboard connected to the database for route revenue and alerts.

## Data source
- **Dataset:** Salvador Unified Network for Transport (SUNT): smart-card fare validations and GTFS routes, stops and trips. https://pypi.org/project/suntdataset/0.1.3/
- **Licence:** to be confirmed before loading (must allow educational use).
- **Privacy:** card IDs are anonymized; no personal data is loaded.
- **Limitation:** the data is not from Rwanda because Kigali fare data is not public. The design follows the Kigali smartcard (Tap&Go) model.

## Innovation
**Option:** Analytics dashboard. **Tool:** Oracle APEX, connected live to the Oracle database. It shows revenue by route and day, trips per bus and open revenue alerts. Business rules stay in PL/SQL.

## Planned tables
| Table | Purpose |
|-------|---------|
| OPERATORS | Bus companies |
| ROUTES | Bus lines with direction and base fare |
| VEHICLES | Buses and their operator, status |
| TRIPS | Each scheduled or completed trip |
| FARE_TRANSACTIONS | Each fare validation (card hash, time, trip, amount) |
| DAILY_REVENUE | Revenue totals per route, vehicle and day |
| REVENUE_ALERTS | Flags for revenue below expected |
| AUDIT_LOG | Who tried what, when, and whether it was allowed |

## Planned PL/SQL features
- **Procedures:** `record_fare` (validates and inserts a fare), `close_day` (builds daily revenue).
- **Functions:** `get_route_revenue`, `get_expected_revenue`.
- **Cursors:** loop over the day's trips to compare actual and expected revenue and raise alerts.
- **Package:** `bus_revenue_pkg` groups the procedures and functions above.
- **Triggers:** block fares on buses that are not in service; block changes to fares of a closed day; write every attempt to the audit log.
- **Exceptions:** custom errors for unknown vehicle, closed day and invalid amount.

## References
See `docs/research/research_log.md`.

## Repository structure
```
docs/research/      research log
docs/proposal/      2-page proposal
docs/presentation/  presentation slides
data/               dataset sample
```
