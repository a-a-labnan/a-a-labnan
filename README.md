<div align="center">
  <img src="./banner.svg" alt="K.B.M. Arak Ayman Labnan — Software Engineer, Mobile" width="100%">
</div>

<div align="center">

**I don't hand off the backend.** I build the Flutter client, the FastAPI service behind it, and the schema underneath that — concept to store release.

[![Play Store](https://img.shields.io/badge/Google_Play-2_apps_live-14213d?style=flat-square&logo=googleplay&logoColor=fca311)](https://play.google.com/store/apps/details?id=com.zuhabul.propertystudio)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-labnan--cse-14213d?style=flat-square&logo=linkedin&logoColor=fca311)](https://www.linkedin.com/in/labnan-cse/)
[![Email](https://img.shields.io/badge/Email-labnan.cse@gmail.com-14213d?style=flat-square&logo=gmail&logoColor=fca311)](mailto:labnan.cse@gmail.com)

</div>

---

## How I build

Most mobile developers stop at the API boundary. I own both sides of it — which means the discount engine lives on the server where it belongs, and the client stays thin.

```mermaid
flowchart LR
  subgraph C["FLUTTER CLIENT"]
    direction TB
    W["Widgets"] --> S["Riverpod / BLoC"]
    S --> R["Repositories"]
    R --> D["Dio"]
  end

  subgraph A["FASTAPI SERVICE"]
    direction TB
    RT["Routers"] --> DL["Domain logic"]
    DL --> OR["SQLModel / SQLAlchemy"]
  end

  D -->|"REST · JSON"| RT
  OR --> PG[("PostgreSQL")]
  A -.->|"Docker Compose"| PG

  classDef c fill:#14213d,stroke:#fca311,stroke-width:1.5px,color:#ffffff
  classDef a fill:#1d2c4c,stroke:#fca311,stroke-width:1.5px,color:#ffffff
  classDef db fill:#fca311,stroke:#14213d,stroke-width:1.5px,color:#14213d
  class W,S,R,D c
  class RT,DL,OR a
  class PG db
```

Both sides layered the same way, because Clean Architecture shouldn't stop at the network call.

---

## Shipped and live

| | What it does | My part |
|---|---|---|
| **[Property Studio](https://play.google.com/store/apps/details?id=com.zuhabul.propertystudio)**<br><sub>1K+ installs · [site](https://propertystudio.com.bd/)</sub> | Operating system for property owners and managers — one app for a single flat or a whole portfolio | Rent and billing automation with late-fee rules, accounting and tax dashboards with unit-level P&L, IoT control for pumps, lighting and lifts — and **Genie**, the in-app AI assistant ([below](#genie--an-llm-feature-that-actually-shipped)) |
| **[Nogora](https://play.google.com/store/apps/details?id=com.nogora.superapp)**<br><sub>Consumer super-app · [site](https://nogora.com/)</sub> | City living in Bangladesh, in one secure place | Rent and utility payments with digital receipts and real-time alerts, photo-based maintenance ticketing, encrypted document vault, category-wise budgeting |
| **Ethical Drugs Sales App**<br><sub>Enterprise · ERP-integrated</sub> | Field-sales client wired into a group-wide ERP | **Sole developer, both sides.** 13 endpoint modules across auth, customers, products, orders and collections. Multi-tier discount engine (ND/FD/SCD/PB) and invoice allocation modelled server-side. GPS-verified order placement, English and Bengali localisation |

---

## Genie — an LLM feature that actually shipped

Inside Property Studio there's a chat assistant called **Genie**. A landlord types *"which tenants are overdue this month?"* and gets a straight answer drawn from their own property data — not a generic chatbot reply.

Plenty of people have wired up a chat completion. The work is everything around it.

```mermaid
flowchart LR
  Q["User question"] --> CTX["Scoped context<br/>tenants · dues · units"]
  CTX --> P["Prompt assembly"]
  P --> LLM["Model"]
  LLM -->|"streamed tokens"| UI["Flutter chat UI"]
  LLM -.->|"timeout · empty · error"| FB["Graceful fallback"]
  FB --> UI

  classDef n fill:#14213d,stroke:#fca311,stroke-width:1.5px,color:#ffffff
  classDef acc fill:#fca311,stroke:#14213d,stroke-width:1.5px,color:#14213d
  classDef warn fill:#1d2c4c,stroke:#fca311,stroke-width:1.5px,color:#c3cfe0
  class Q,CTX,P,LLM n
  class UI acc
  class FB warn
```

**Prompt design** — the assistant answers about *this* user's rent, dues, tenants and units, so the real problem is deciding what context to assemble per question and keeping it scoped, relevant and small.

**Streaming responses** — tokens render as they arrive rather than after a spinner. In Flutter that means handling partial state, mid-stream cancellation when the user navigates away, and a chat surface that doesn't jank while rebuilding on every chunk.

**Graceful fallback** — the interesting engineering is the unhappy path. Timeouts, empty completions, malformed output and rate limits all resolve to something useful on screen instead of a stack trace. This is where three years of QA earns its keep: I built the failure modes first.

Live on Google Play, in front of real users, on real property data.

---

## Career

| | Role | Where |
|---|---|---|
| **Dec 2025 — now** | Mobile App Developer | **Sysnova Information Systems** — sister concern of Kazi Farms Group, Dhaka. Production Flutter across Android and iOS for enterprise-scale applications, plus the FastAPI services behind them |
| **Feb — Nov 2025** | Software Engineer, Flutter | **Property Studio**, Dhaka. Core modules of a property platform now past 1K installs — billing automation, accounting dashboards, the IoT control layer |
| **Oct 2021 — Dec 2024** | Senior QA Engineer | **Vcube Soft and Tech**, Dhaka. Test planning across mobile and web release cycles, Selenium regression automation, API validation, defect triage |

Three years testing other people's software, then two building my own. The order turned out to matter.

---

## Stack

<details>
<summary><b>Mobile</b> — Flutter, Dart, and whichever state pattern the problem actually needs</summary>
<br>

![Flutter](https://img.shields.io/badge/Flutter-02569B?style=flat-square&logo=flutter&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-0175C2?style=flat-square&logo=dart&logoColor=white)
![Riverpod](https://img.shields.io/badge/Riverpod-3d5afe?style=flat-square)
![BLoC](https://img.shields.io/badge/BLoC-1a73e8?style=flat-square)
![GetX](https://img.shields.io/badge/GetX-8a2be2?style=flat-square)
![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=flat-square&logo=firebase&logoColor=black)

GoRouter for navigation, Dio for transport. I pick Riverpod for new work and stay fluent in BLoC, GetX and Provider because inherited codebases don't ask your preference.

</details>

<details>
<summary><b>Backend</b> — Python, FastAPI, PostgreSQL, containerised</summary>
<br>

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-D71F00?style=flat-square&logo=sqlalchemy&logoColor=white)
![Pydantic](https://img.shields.io/badge/Pydantic-E92063?style=flat-square&logo=pydantic&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

SQLModel over SQLAlchemy, Pydantic for schema validation, Alembic for migrations. Docker Compose so the whole stack comes up with one command.

</details>

<details>
<summary><b>Quality</b> — three years of QA, still shaping how I build</summary>
<br>

![Selenium](https://img.shields.io/badge/Selenium-43B02A?style=flat-square&logo=selenium&logoColor=white)
![Postman](https://img.shields.io/badge/Postman-FF6C37?style=flat-square&logo=postman&logoColor=white)
![Jira](https://img.shields.io/badge/Jira-0052CC?style=flat-square&logo=jira&logoColor=white)

I spent three years as a QA engineer, finishing as senior — test planning across mobile and web release cycles, Selenium regression suites, API validation, defect triage.

It's the most useful thing on this page. I design for the edge case while the feature is still on the whiteboard, not after someone files a ticket. Unit and widget tests go in before the release candidate, not after it. A regression-free release is part of shipping the feature — not a phase that follows it.

</details>

---

## Working with AI

![Claude Code](https://img.shields.io/badge/Claude_Code-D97757?style=flat-square&logo=anthropic&logoColor=white)
![Copilot](https://img.shields.io/badge/GitHub_Copilot-000000?style=flat-square&logo=githubcopilot&logoColor=white)
![Cursor](https://img.shields.io/badge/Cursor-000000?style=flat-square)

Daily AI pair-programming for scaffolding, boilerplate and test generation. The discipline matters more than the tooling: every suggestion gets reviewed and covered by tests before it merges. Generated code that nobody read is just technical debt that arrived faster.

---

## Working remotely

Based in **Dhaka, UTC+6** — which lines up better with more of the world than people assume.

| Region | Daily overlap on a normal Dhaka workday |
|---|---|
| Gulf (UTC+3/+4) | **~8 hours** |
| Central Europe (UTC+2) | **~6 hours** |
| UK (UTC+1) | **~5 hours** |

**English** — professional working proficiency, written and spoken. **Bangla** — native.

Comfortable working async: written standups, decisions recorded in the PR, and enough detail in a handover that nobody has to wait for my morning.

<details>
<summary><b>Education and training</b></summary>
<br>

**BSc in Computer Science and Engineering** — Daffodil International University, 2017–2021. CGPA 3.37 / 4.00. Placed 4th in C programming at the DIU Take-off Programming Contest.

**Software Testing and Quality Assurance** — Skill Jobs, Dhaka, 2022. Certificate SJ/SQA-20220080033.

**Ongoing** — Clean Architecture and SOLID in Flutter, advanced state-management patterns, Python and FastAPI.

</details>

---

<div align="center">
<sub>Currently deepening Clean Architecture in Flutter and building out the FastAPI side of my stack.<br>Interested in remote work with international teams.</sub>
</div>
