# Manager Library — Infrastructure Environment

This repository contains the containerized orchestration and network layout for *Manager Library*, deploying a clean reference environment using **Docker** and **Docker Compose**.

## ⚙️ Core SDD Architectural Decisions

Following the strict environment requirements outlined in the business specification documents, this infrastructure layer enforces the following constraints:

### 1. Database Engine Isolation
- **Reference Database Engine:** Deploys a lightweight, official **PostgreSQL 16** server instance (`postgres:16-alpine`) as demanded by the physical layout parameters.
- **Strict UTC Server Enforcement:** Enforces absolute timezone synchronization by applying `TZ: UTC` directly onto the engine container container environment variable block. This guarantees all `timestamptz` inputs and outputs maintain absolute audit consistency.
- **Pristine Schema Initial State:** The database starts completely empty by design. The structural tables, uniqueness indices, and soft deletion bounds are sequentially injected dynamically by the Laravel backend framework migration routines.
- **Volume Persistency Layer:** Binds database blocks to an isolated local named volume (`pgdata`) to protect core entity tables from state loss during routine runtime recycling.

