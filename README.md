# Orchestrating Workflows for GenAI Applications with Apache Airflow

This repository demonstrates how to orchestrate workflows for GenAI applications using Apache Airflow. Focus is on transforming prototype code into production-ready, automated pipelines.

## Notebook

### rag_prototype.ipynb - RAG Prototype
- Comprehensive implementation of a Retrieval Augmented Generation (RAG) system:
  - Book recommendation system using semantic search
  - Vector database integration with Weaviate
  - Text embedding generation using BAAI/bge-small-en model
- Data Processing Pipeline Components:
  - Reading and parsing book descriptions from text files
  - Text preprocessing and formatting
  - Converting book descriptions into vector embeddings
  - Storing embeddings in Weaviate vector database
- Search and Retrieval Implementation:
  - Semantic similarity search using vector embeddings
  - Near-vector search capabilities
  - Book recommendations based on query similarity
- System Architecture:
  - Input: Text files containing book descriptions (title, author, description)
  - Processing: Text to vector conversion using embedding model
  - Storage: Weaviate vector database for efficient similarity search
  - Output: Relevant book recommendations based on user queries
- Foundation for Advanced Pipeline Development:
  - Base implementation that will be automated
  - Core functionality for data processing and retrieval
  - Integration points for Airflow orchestration

## Python Scripts

### Production DAGs

#### fetch_data.py - Data Ingestion and Processing Pipeline
A robust, production-ready DAG that handles the complete data processing pipeline:

- **Scheduling and Execution**:
  - Runs hourly (configurable via `schedule="@hourly"`)
  - DAG-level retries with 10-second delay
  - Custom failure callbacks for monitoring and alerting

- **Task Structure and Features**:
  1. `create_collection_if_not_exists`:
     - Initializes Weaviate collection for book data
     - Enhanced with 5 retries and 2-second retry delay
     - Robust error handling with failure callbacks

  2. `list_book_description_files`:
     - Scans for text files containing book descriptions
     - Dynamic input processing capabilities

  3. `transform_book_description_files`:
     - Parallel processing using dynamic task mapping
     - Extracts and structures book metadata (title, author, description)
     - Processes multiple files concurrently for improved efficiency

  4. `create_vector_embeddings`:
     - Generates embeddings using BAAI/bge-small-en model
     - Parallel processing of book descriptions
     - Optimized for batch processing

  5. `load_embeddings_to_vector_db`:
     - Bulk loading to Weaviate vector database
     - Asset-aware with data tracking
     - Resilient execution with "all_done" trigger rule
     - Handles partial successes in upstream tasks

#### query_data.py - Semantic Search Pipeline
An intelligent search pipeline that leverages vector embeddings:

- **Scheduling and Triggers**:
  - Data-aware scheduling using Assets
  - Automatically triggers when new data is available
  
- **Features**:
  - Parameterized queries through Airflow UI
  - Real-time vector similarity search
  - Integration with Weaviate for efficient retrieval
  - Customizable search results with configurable limits

- **Implementation Details**:
  - Uses the same embedding model (BAAI/bge-small-en)
  - Contextual parameter handling
  - Clean output formatting for book recommendations

## Setup and Requirements

### Prerequisites
- Python environment (virtual environment recommended)
- Docker Desktop (for running Airflow and Weaviate)
- Astro CLI (for local Airflow development)

### Environment Setup
1. Airflow credentials:
   - Username: `airflow`
   - Password: `airflow`

2. Key Components:
   - Weaviate vector database
   - FastEmbed for text embeddings
   - Apache Airflow for workflow orchestration

### Directory Structure
```
├── dags/
│   └── genai_dags/
│       ├── fetch_data.py
│       └── query_data.py
├── include/
│   └── data/
│       ├── book_descriptions_1.txt
│       └── book_descriptions_2.txt
└── notebooks/
    └── rag_prototype.ipynb
```

## Resources and References
- [Airflow Documentation](https://airflow.apache.org/docs/)
- [Astronomer Documentation](https://www.astronomer.io/docs/)
- [Weaviate Documentation](https://weaviate.io/developers/weaviate)
- [Setup for Airflow and Weaviate](https://github.com/astronomer/orchestrating-workflows-for-genai-deeplearning-ai) 


## Credits

This project is based on materials from the excellent [Orchestrating Workflows for GenAI Applications]course by deeplearning.ai. Special thanks to the deeplearning.ai team for providing such high-quality educational resources. If you want to learn more about GenAI workflows and Airflow, check out their courses and content!
