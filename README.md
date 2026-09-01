<div align="center">
  <img src="./banner.svg" alt="K.B.M. Arak Ayman Labnan — Software Engineer, Mobile" width="100%">
</div>

<div align="center">
  <img src="./focus.svg" alt="Now building: Flutter clients that don't jank, the FastAPI services behind them, the failure modes first" width="100%">
</div>

<br>

<div align="center">

### **I don't hand off the backend.**

Flutter client. FastAPI service. The schema underneath it.<br>
Concept to store release — no seams, no "that's the other team's problem."

<br>

[![Play Store](https://img.shields.io/badge/Google_Play-2_apps_live-14213d?style=for-the-badge&logo=googleplay&logoColor=fca311&labelColor=0d1526)](https://play.google.com/store/apps/details?id=com.zuhabul.propertystudio)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-labnan--cse-14213d?style=for-the-badge&logo=linkedin&logoColor=fca311&labelColor=0d1526)](https://www.linkedin.com/in/labnan-cse/)
[![Email](https://img.shields.io/badge/Email-labnan.cse-14213d?style=for-the-badge&logo=gmail&logoColor=fca311&labelColor=0d1526)](mailto:labnan.cse@gmail.com)

</div>

<img src="./divider.svg" width="100%" alt="">

<div align="center">
  <img src="./impact.svg" alt="2 apps live on Google Play · 1K+ installs · 5 years: 3 breaking, 2 building · 13 API modules shipped solo" width="100%">
</div>

<img src="./divider.svg" width="100%" alt="">

## Both sides of the API

Most mobile developers stop at the network boundary. I own what's on the other side of it — which is why the discount engine lives on the server where it belongs, and the client stays thin enough to reason about.

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

Same layering on both sides — because Clean Architecture shouldn't stop at the network call.

<img src="./divider.svg" width="100%" alt="">

## Shipped. Live. On real phones.

| | What it does | What I built |
|---|---|---|
| **[Property Studio](https://play.google.com/store/apps/details?id=com.zuhabul.propertystudio)**<br><sub>1K+ installs · [site](https://propertystudio.com.bd/)</sub> | An operating system for property owners and managers — one app for a single flat or a whole portfolio | Rent and billing automation with late-fee rules, accounting and tax dashboards with unit-level P&L, IoT control for pumps, lighting and lifts — and **Genie**, the in-app AI assistant ([below](#genie--the-llm-feature-that-actually-shipped)) |
| **[Nogora](https://play.google.com/store/apps/details?id=com.nogora.superapp)**<br><sub>Consumer super-app · [site](https://nogora.com/)</sub> | City living in Bangladesh, in one secure place | Rent and utility payments with digital receipts and real-time alerts, photo-based maintenance ticketing, encrypted document vault, category-wise budgeting |
| **Ethical Drugs Sales App**<br><sub>Enterprise · ERP-integrated</sub> | Field-sales client wired into a group-wide ERP | **Sole developer, both sides.** 13 endpoint modules across auth, customers, products, orders and collections. Multi-tier discount engine (ND/FD/SCD/PB) and invoice allocation modelled server-side. GPS-verified order placement, English and Bengali localisation |

<img src="./divider.svg" width="100%" alt="">

## Genie — the LLM feature that actually shipped

Inside Property Studio there's a chat assistant called **Genie**. A landlord types *"which tenants are overdue this month?"* and gets a straight answer pulled from their own property data — not a generic chatbot reply.

Anyone can wire up a chat completion. The work is everything around it.

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

**Prompt design** — the assistant answers about *this* user's rent, dues, tenants and units. The real problem is deciding what context to assemble per question, and keeping it scoped, relevant and small.

**Streaming responses** — tokens render as they arrive instead of behind a spinner. In Flutter that means partial state, mid-stream cancellation when the user navigates away, and a chat surface that doesn't jank while rebuilding on every chunk.

**Graceful fallback** — the interesting engineering is the unhappy path. Timeouts, empty completions, malformed output and rate limits all resolve to something useful on screen instead of a stack trace. This is where three years of QA earns its keep: I built the failure modes first.

Live on Google Play. Real users. Real property data.

<img src="./divider.svg" width="100%" alt="">

## What GitHub knows

<div align="center">

<img height="170" src="https://github-profile-summary-cards.vercel.app/api/cards/stats?username=a-a-labnan&bg_color=0d1526&title_color=fca311&text_color=c3cfe0&icon_color=fca311&border_color=0d1526" alt="GitHub stats">
<img height="170" src="https://github-profile-summary-cards.vercel.app/api/cards/most-commit-language?username=a-a-labnan&bg_color=0d1526&title_color=fca311&text_color=c3cfe0&icon_color=fca311&border_color=0d1526" alt="Top languages">

<br><br>

<img height="170" src="https://streak-stats.demolab.com?user=a-a-labnan&hide_border=true&background=0d1526&border=fca311&stroke=fca311&ring=fca311&fire=fca311&currStreakLabel=fca311&sideLabels=c3cfe0&currStreakNum=ffffff&sideNums=ffffff&dates=8a99b0" alt="Contribution streak">

</div>

<img src="./divider.svg" width="100%" alt="">

## How I got here

| | Role | Where |
|---|---|---|
| **Dec 2025 — now** | Mobile App Developer | **Sysnova Information Systems** — sister concern of Kazi Farms Group, Dhaka. Production Flutter across Android and iOS for enterprise-scale applications, plus the FastAPI services behind them |
| **Feb — Nov 2025** | Software Engineer, Flutter | **Property Studio**, Dhaka. Core modules of a property platform now past 1K installs — billing automation, accounting dashboards, the IoT control layer |
| **Oct 2021 — Dec 2024** | Senior QA Engineer | **Vcube Soft and Tech**, Dhaka. Test planning across mobile and web release cycles, Selenium regression automation, API validation, defect triage |

Three years breaking other people's software, then two building my own. The order turned out to matter.

<img src="./divider.svg" width="100%" alt="">

## The toolbox

<details>
<summary><b>Mobile</b> — Flutter, Dart, and whichever state pattern the problem actually needs</summary>
<br>

![Flutter](https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-0175C2?style=for-the-badge&logo=dart&logoColor=white)
![Riverpod](https://img.shields.io/badge/Riverpod-3d5afe?style=for-the-badge)
![BLoC](https://img.shields.io/badge/BLoC-1a73e8?style=for-the-badge)
![GetX](https://img.shields.io/badge/GetX-8a2be2?style=for-the-badge)
![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)

GoRouter for navigation, Dio for transport. Riverpod for new work, and I stay fluent in BLoC, GetX and Provider — inherited codebases don't ask your preference.

</details>

<details>
<summary><b>Backend</b> — Python, FastAPI, PostgreSQL, containerised</summary>
<br>

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-D71F00?style=for-the-badge&logo=sqlalchemy&logoColor=white)
![Pydantic](https://img.shields.io/badge/Pydantic-E92063?style=for-the-badge&logo=pydantic&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

SQLModel over SQLAlchemy, Pydantic for schema validation, Alembic for migrations. Docker Compose so the whole stack comes up with one command.

</details>

<details>
<summary><b>Quality</b> — three years of QA, still shaping how I build</summary>
<br>

![Selenium](https://img.shields.io/badge/Selenium-43B02A?style=for-the-badge&logo=selenium&logoColor=white)
![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)
![Jira](https://img.shields.io/badge/Jira-0052CC?style=for-the-badge&logo=jira&logoColor=white)

Three years as a QA engineer, finishing as senior — test planning across mobile and web release cycles, Selenium regression suites, API validation, defect triage.

It's the most useful thing on this page. I design for the edge case while the feature is still on the whiteboard, not after someone files a ticket. Unit and widget tests go in before the release candidate, not after it. A regression-free release is part of shipping the feature — not a phase that follows it.

</details>

<details>
<summary><b>AI in the loop</b> — daily pair-programming, reviewed like any other diff</summary>
<br>

![Claude Code](https://img.shields.io/badge/Claude_Code-D97757?style=for-the-badge&logo=anthropic&logoColor=white)
![Copilot](https://img.shields.io/badge/GitHub_Copilot-000000?style=for-the-badge&logo=githubcopilot&logoColor=white)
![Cursor](https://img.shields.io/badge/Cursor-000000?style=for-the-badge)

Scaffolding, boilerplate, test generation. The discipline matters more than the tooling: every suggestion gets reviewed and covered by tests before it merges. Generated code nobody read is just technical debt that arrived faster.

</details>

<img src="./divider.svg" width="100%" alt="">

## Credentials you can click

<div align="center">

[![Flutter and AI — Completion](https://img.shields.io/badge/Ostad-Flutter_and_AI_%E2%80%94_Completion-14213d?style=for-the-badge&logo=flutter&logoColor=fca311&labelColor=0d1526)](https://ostad.app/share/certificate/c38990-k.b.m.-arak-ayman-labnan)
[![Flutter and AI — Performance](https://img.shields.io/badge/Ostad-Flutter_and_AI_%E2%80%94_Performance-14213d?style=for-the-badge&logo=flutter&logoColor=fca311&labelColor=0d1526)](https://ostad.app/share/certificate/c40001-k.b.m.-arak-ayman-labnan)
![Software QA — Skill Jobs](https://img.shields.io/badge/Skill_Jobs-Software_Testing_and_QA-14213d?style=for-the-badge&logo=selenium&logoColor=fca311&labelColor=0d1526)

</div>

| | Certificate | Issuer | Verify |
|---|---|---|---|
| **2025** | **App Development with Flutter & AI**<br><sub>Two certificates: course completion, and performance</sub> | Ostad, Dhaka | [completion ↗](https://ostad.app/share/certificate/c38990-k.b.m.-arak-ayman-labnan) · [performance ↗](https://ostad.app/share/certificate/c40001-k.b.m.-arak-ayman-labnan) |
| **2022** | **Software Testing and Quality Assurance** | Skill Jobs, Dhaka | `SJ/SQA-20220080033` |

Ostad issues two certificates for that course — one for finishing it, one for how it was finished. The AI half of the syllabus is what became **Genie**, the LLM assistant now live inside Property Studio.

**Currently studying** — Clean Architecture and SOLID in Flutter, advanced state-management patterns, Python and FastAPI. **Just started on machine learning** — the fundamentals, from the Python side I already work in.

<img src="./divider.svg" width="100%" alt="">

## Remote, and actually overlapping

Based in **Dhaka, UTC+6** — which lines up with more of the world than people assume.

| Region | Daily overlap on a normal Dhaka workday |
|---|---|
| Gulf (UTC+3/+4) | **~8 hours** |
| Central Europe (UTC+2) | **~6 hours** |
| UK (UTC+1) | **~5 hours** |

**English** — professional working proficiency, written and spoken. **Bangla** — native.

Comfortable async: written standups, decisions recorded in the PR, and enough detail in a handover that nobody has to wait for my morning.

<details>
<summary><b>Education and training</b></summary>
<br>

| | Qualification | Institution | Result |
|---|---|---|---|
| **2017 — 2021** | BSc in Computer Science and Engineering | Daffodil International University | CGPA **3.37 / 4.00** |
| **2014 — 2015** | Higher Secondary School Certificate | Cantonment Public School & College, Saidpur | GPA **5.00 / 5.00** |
| **2012 — 2013** | Secondary School Certificate | Thakurgaon Govt. Boys' High School | GPA **5.00 / 5.00** |

Placed **4th in C programming** at the DIU Take-off Programming Contest, Summer 2017 — first semester, first contest.

Certificates live in [Credentials you can click](#credentials-you-can-click) above.

</details>

<img src="./divider.svg" width="100%" alt="">

<div align="center">

**Currently** deepening Clean Architecture in Flutter and building out the FastAPI side of the stack.<br>
**Open to** remote work with international teams.

<br>

[![Email](https://img.shields.io/badge/Say_hello-labnan.cse@gmail.com-fca311?style=for-the-badge&logo=gmail&logoColor=0d1526&labelColor=14213d)](mailto:labnan.cse@gmail.com)

</div>
