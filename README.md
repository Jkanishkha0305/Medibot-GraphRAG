# MediBot-GraphRAG

A **GraphRAG-based chatbot** built using **LangChain** and **Neo4j**, designed for hospital systems. The chatbot retrieves structured and unstructured data about **patients, visits, physicians, insurance payers, and hospital locations**. This project also explores integrating **graph databases** and deploying the chatbot using **FastAPI & Streamlit**.

## 🚀 Features
- **GraphRAG (Graph Retrieval-Augmented Generation)** for querying hospital data.
- **LangChain-powered chatbot** for patient and hospital-related inquiries.
- **Neo4j graph database integration** for structured data retrieval.
- **FastAPI-based API** for backend services.
- **Streamlit frontend** for chatbot interaction.
- **ETL pipeline for Neo4j** to handle hospital data ingestion.
- **Dockerized deployment** for seamless integration and scaling.

## 📂 Project Structure
```
└── jkanishkha0305-medibot-graphrag/
    ├── README.md
    ├── docker-compose.yml
    ├── requirements.txt
    ├── chatbot_api/
    │   ├── Dockerfile
    │   ├── pyproject.toml
    │   └── src/
    │       ├── entrypoint.sh
    │       ├── main.py
    │       ├── agents/
    │       │   └── hospital_rag_agent.py
    │       ├── chains/
    │       │   ├── hospital_cypher_chain.py
    │       │   └── hospital_review_chain.py
    │       ├── models/
    │       │   └── hospital_rag_query.py
    │       ├── tools/
    │       │   └── wait_times.py
    │       └── utils/
    │           └── async_utils.py
    ├── chatbot_frontend/
    │   ├── Dockerfile
    │   ├── pyproject.toml
    │   └── src/
    │       ├── entrypoint.sh
    │       └── main.py
    ├── data/
    │   ├── data_exploration.ipynb
    │   ├── hospitals.csv
    │   ├── patients.csv
    │   ├── payers.csv
    │   ├── physicians.csv
    │   ├── reviews.csv
    │   └── visits.csv
    ├── hospital_neo4j_etl/
    │   ├── Dockerfile
    │   ├── pyproject.toml
    │   └── src/
    │       ├── entrypoint.sh
    │       └── hospital_bulk_csv_write.py
    └── tests/
        ├── async_agent_requests.py
        └── sync_agent_requests.py
```

## 🛠️ Installation & Setup
### Prerequisites
- Python 3.8+
- Docker & Docker Compose
- Neo4j

### Clone the Repository
```sh
git clone https://github.com/jkanishkha0305/medibot-graphrag.git
cd medibot-graphrag
```

### Install Dependencies
```sh
pip install -r requirements.txt
```

### Set Up Environment Variables
Create a `.env` file and define:
```sh
NEO4J_URI=bolt://localhost:7687
NEO4J_USERNAME=neo4j
NEO4J_PASSWORD=password
OPENAI_API_KEY=your_api_key
```

### Start Services using Docker Compose
```sh
docker-compose up --build
```

## 🚀 Usage
### Start the API
```sh
cd chatbot_api/src
uvicorn main:app --host 0.0.0.0 --port 8000
```

### Run the Frontend
```sh
cd chatbot_frontend/src
streamlit run main.py
```

## 🧪 Running Tests
To test API requests:
```sh
python tests/sync_agent_requests.py
```

## 🤝 Contributing
Feel free to fork, open issues, or submit pull requests!

## 📜 License
This project is licensed under the MIT License.
