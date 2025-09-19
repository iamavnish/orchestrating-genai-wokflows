# Orchestrating Workflows for GenAI Applications with Apache Airflow
This repository contains a series of Jupyter notebooks that demonstrate how to orchestrate workflows for GenAI applications using Apache Airflow. Focus is on transforming prototype code into production-ready, automated pipelines.

## Notebook Contents

### L2.ipynb - RAG Prototype
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
  - Base implementation that will be automated in later lessons
  - Core functionality for data processing and retrieval
  - Integration points for Airflow orchestration

### L3.ipynb - Building a Simple Pipeline
- Introduction to basic Airflow concepts and syntax
- Overview of Airflow components and architecture:
  - DAG Processor
  - Scheduler
  - Workers
  - Metadata Database
  - API Server/UI
- Creating first DAGs with tasks:
  - Simple 2-task and 3-task DAG examples
  - Task dependencies and data flow
  - Using the `@dag` and `@task` decorators
  - Implementing task chaining with `chain()`
- Introduction to Airflow UI and basic operations

### L4.ipynb - Turning Your Notebook Into a Pipeline
- Transforming the RAG prototype into production DAGs
- Creating two main DAGs:
  1. `fetch_data`: Pipeline for data ingestion and processing
     - Creating vector database collections
     - Listing and transforming book description files
     - Generating vector embeddings
     - Loading embeddings into the vector database
  2. `query_data`: Pipeline for querying the vector database
     - Implementing semantic search functionality
     - Processing and returning search results
- Integration with Weaviate vector database
- Using the BAAI/bge-small-en embedding model
- Working with Airflow connections and hooks

### L5.ipynb - Scheduling and DAG Parameters
- Introduction to different scheduling strategies:
  - Time-based scheduling (using cron expressions and presets)
  - Data-aware scheduling using Assets
- Implementing scheduled DAGs:
  - Setting up hourly schedule for data fetching
  - Configuring Asset-based triggers
- Working with DAG parameters:
  - Adding customizable query parameters
  - Using context variables in tasks
  - Handling user inputs through the Airflow UI
- Advanced Asset management:
  - Creating Asset events
  - Asset-based dependencies between DAGs
  - Monitoring Asset updates

### L6.ipynb - Making the Pipeline Adaptable
- Introduction to Dynamic Task Mapping
- Understanding parallel task execution
- Improving the fetch_data DAG:
  - Converting sequential processing to parallel execution
  - Processing multiple book description files concurrently
  - Optimizing vector embedding generation
- Implementation of:
  - Dynamic task generation based on input files
  - Parallel processing of book descriptions
  - Efficient vector embedding creation
  - Improved error handling and resilience
- Example of simple dynamic mapping
- Practical demonstration with book processing pipeline

### L7.ipynb - Prepare to Fail
- Implementing robust error handling strategies:
  - Task failure simulation and testing
  - Configuring retry mechanisms
  - Setting retry delays and attempts
- Advanced failure handling:
  - DAG-level retry configurations
  - Task-specific retry settings
  - Implementing failure callbacks
- Trigger rule configurations:
  - Understanding different trigger rules
  - Using "all_done" trigger rule for resilient execution
- Error notification system:
  - Custom callback functions
  - Failure notifications and alerting
  - Context-aware error handling
- Best practices for production pipelines:
  - Error recovery strategies
  - Monitoring and notification setup
  - Maintaining pipeline reliability

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
│   ├── fetch_data.py
│   ├── query_data.py
├── include/
│   └── data/
│       ├── book_descriptions_1.txt
│       └── book_descriptions_2.txt
└── notebooks/
    ├── L2.ipynb
    ├── L3.ipynb
    ├── L4.ipynb
    ├── L5.ipynb
    └── L6.ipynb
```

## Resources and References
- [Airflow Documentation](https://airflow.apache.org/docs/)
- [Astronomer Documentation](https://www.astronomer.io/docs/)
- [Weaviate Documentation](https://weaviate.io/developers/weaviate)
- [Local setup for Airflow and Weaviate](https://github.com/astronomer/orchestrating-workflows-for-genai-deeplearning-ai) 


## Credits

This project and its notebooks are based on materials from the excellent [Orchestrating Workflows for GenAI Applications](https://www.deeplearning.ai/) course by deeplearning.ai. Special thanks to the deeplearning.ai team for providing high-quality educational resources and making these notebooks available for download. If you want to learn more about GenAI workflows and Airflow, check out their courses and content!
