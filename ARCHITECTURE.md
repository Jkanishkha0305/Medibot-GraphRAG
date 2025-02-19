# Architecture — Medibot-GraphRAG

## System Overview

```
┌─────────────────────────────────────────────────────────┐
│                    Medibot-GraphRAG                      │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  User Query                                             │
│      │                                                  │
│      ▼                                                  │
│  ┌──────────────┐    ┌─────────────────────────────┐   │
│  │  Streamlit   │───▶│      FastAPI Backend         │   │
│  │  Frontend    │    │   (hospital_rag_agent.py)    │   │
│  └──────────────┘    └──────────┬──────────────────┘   │
│                                 │                        │
│                    ┌────────────▼────────────┐          │
│                    │    LangChain Agents      │          │
│                    │  ┌──────────────────┐   │          │
│                    │  │  Cypher Chain    │   │          │
│                    │  │  (structured Q)  │   │          │
│                    │  └────────┬─────────┘   │          │
│                    │  ┌────────▼─────────┐   │          │
│                    │  │   Review Chain   │   │          │
│                    │  │  (unstructured)  │   │          │
│                    │  └────────┬─────────┘   │          │
│                    └──────────┬──────────────┘          │
│                               │                          │
│                    ┌──────────▼──────────┐              │
│                    │     Neo4j Graph DB   │              │
│                    │  Patients · Doctors  │              │
│                    │  Payers · Hospitals  │              │
│                    └─────────────────────┘              │
│                                                         │
│  ETL Pipeline: CSV → hospital_bulk_csv_write → Neo4j   │
└─────────────────────────────────────────────────────────┘
```

## Components

| Component | Path | Responsibility |
|-----------|------|----------------|
| FastAPI backend | `chatbot_api/src/main.py` | REST API, agent orchestration |
| Hospital RAG Agent | `chatbot_api/src/agents/` | LangChain multi-agent routing |
| Cypher Chain | `chatbot_api/src/chains/hospital_cypher_chain.py` | Structured Neo4j queries |
| Review Chain | `chatbot_api/src/chains/hospital_review_chain.py` | Unstructured text retrieval |
| ETL Pipeline | `hospital_neo4j_etl/` | Bulk load CSV data → Neo4j |
| Streamlit UI | `chatbot_frontend/` | User-facing chat interface |

## Data Model (Neo4j Graph)

```
(Patient)-[:HAS_VISIT]->(Visit)
(Visit)-[:AT]->(Hospital)
(Visit)-[:TREATED_BY]->(Physician)
(Visit)-[:COVERED_BY]->(Payer)
(Hospital)-[:LOCATED_IN]->(Location)
```
