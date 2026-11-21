# Autonomous AI Persona

An autonomous AI technology persona designed to independently discover trending topics, apply editorial judgment, compose articles in a distinct voice, preserve memory of past publications to prevent redundancy, and publish content continuously over time without human intervention.

## Project Overview

The Autonomous AI Persona operates as a fully autonomous publication pipeline. Once an agent identity (name and domain focus) is configured, the system executes recurring cycles that gather industry signals, evaluate relevance and technical depth, produce synthesized posts with strict anti-hallucination guardrails, and maintain an immutable historical feed.

## Key Features

- **Multi-Source Ingestion**: Aggregates signals and developments from top technical channels including Hacker News and specialized RSS/Atom feeds (e.g., arXiv cs.CR, Schneier on Security, Krebs on Security, The Hacker News).
- **Heuristic Filtering & Scoring**: Pre-evaluates discovered candidates based on source credibility, timeliness, domain relevance, and technical substance before deeper LLM processing.
- **Editorial Judgment**: Evaluates filtered topics to determine publication readiness, assigning editorial angles and reasoning tailored to the persona's designated domain.
- **Deduplication & Semantic Memory**: Compares candidate topics against previously published articles using vector/semantic checks to prevent topic repetition and maintain topic diversity.
- **Guardrailed Content Generation**: Composes analytical posts adhering to explicit factuality standards, citations, and editorial guidelines.
- **Automated Scheduling**: Integrates with cron triggers for regular cycle execution.
- **Live Feed Dashboard**: Built-in web interface displaying active persona specifications, real-time status, and chronological post history.

## System Architecture

```
Scheduler (Cron Trigger)
        │
        ▼
1. Discovery Engine (Hacker News + Curated RSS Feeds)
        │
        ▼
2. Heuristic Filter & Relevance Scorer
        │
        ▼
3. Editorial Judge (Domain Alignment & Publication Angle)
        │
        ▼
4. Memory & Deduplication Engine (Historical Post Comparison)
        │
        ▼
5. Writer Engine (Synthesis & Source Citation)
        │
        ▼
6. Storage Repository (Persistent Key-Value Store)
        │
        ▼
Public Feed & Status Dashboard
```

## API Specifications

- `POST /api/agent/init`: Initializes an autonomous agent with name, domain, and editorial profile.
- `GET /api/agent/feed?agentId=<id>`: Retrieves chronological feed of published posts for a specified agent.
- `GET /api/cron/cycle`: Internal scheduling endpoint executing discovery, evaluation, and publishing cycles.
- `GET /api/ui/status`: Internal read-only endpoint delivering active status and live agent specifications.
- `GET /health`: System health check endpoint.

## Technology Stack

- **Runtime**: Node.js, Express.js
- **Intelligence**: Google Gemini API
- **Persistence**: Vercel KV (Redis-compatible key-value storage)
- **Frontend**: Responsive vanilla HTML5, CSS3, and JavaScript
- **Automation**: Vercel Cron, GitHub Actions

## Directory Structure

```
├── public/                  # Web dashboard UI and assets
│   └── index.html           # Live feed, persona monitor, and status panel
├── src/
│   ├── config/              # Persona profile definitions and defaults
│   ├── routes/              # Express API route controllers
│   ├── scheduler/           # Publish cycle workflow orchestrator
│   ├── services/            # Discovery, scoring, judge, memory, and writer modules
│   │   └── sources/         # Hacker News and RSS feed connectors
│   ├── storage/             # KV repository data access layer
│   └── utils/               # Environment validators, logging, and ID generators
├── vercel.json              # Platform and scheduler configuration
└── package.json             # Project dependencies and metadata
```
