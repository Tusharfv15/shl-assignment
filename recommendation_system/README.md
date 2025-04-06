# SHL Assessment Recommender System

A recommendation system that suggests the most suitable SHL assessments based on job descriptions or requirements.

## Features

- **Natural Language Querying**: Submit job descriptions or requirements as plain text
- **URL Support**: Process job descriptions directly from URLs
- **Filtering**: Filter assessments by remote testing, adaptive/IRT support, and test types
- **Semantic Search**: Uses OpenAI embeddings for accurate semantic matching
- **Enhanced Mode**: Utilizes GPT for better query understanding and matching
- **Streamlit Web Interface**: Easy-to-use UI for interacting with the system

## System Architecture

The system uses a Retrieval-Augmented Generation (RAG) approach with the following components:

1. **Data Processing**: Cleans and combines assessment attributes into a comprehensive text field
2. **Embedding & Storage**: Generates embeddings using OpenAI's text-embedding-ada-002 model
3. **Vector Storage**: Uses Qdrant for efficient similarity search
4. **Retrieval System**:
   - Basic Mode: Converts the query to an embedding and performs similarity search
   - Enhanced Mode: Uses GPT to better understand the query before similarity search
5. **Streamlit Interface**: Provides a user-friendly web interface for querying and filtering

## Installation

1. Clone the repository
2. Create a virtual environment:
   ```
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
3. Install the required packages:
   ```
   pip install -r requirements.txt
   ```
4. Create a `.env` file with your OpenAI API key:
   ```
   OPENAI_API_KEY=your_api_key_here
   ```

## Usage

### Building Embeddings

Before using the system, you need to build the embeddings for your assessment data:

```
python main.py build --data-file data/shl_assessments.csv
```

### Using the Web Interface

Launch the Streamlit web interface:

```
python run_app.py
```

This will start a web server at http://localhost:8501 where you can:

1. Enter a job description or URL
2. Set filtering options
3. Get assessment recommendations

### Command Line Interface

You can also use the system from the command line:

```
# Basic recommendation
python main.py recommend "We need an account manager who can manage client relationships"

# With filters
python main.py recommend "Looking for a sales director" --remote-testing Yes --test-types "Competencies,Personality & Behavior"

# Enhanced mode with GPT
python main.py recommend "Need someone who can lead a team of account managers" --enhanced

# Save results to file
python main.py recommend "Technical project manager position" --output results.json
```

## Evaluation

The system includes evaluation metrics to measure performance:

```
python main.py evaluate --queries-file data/sample_test_queries.json
```

This calculates:

- Mean Recall@K: Measures how many relevant assessments are found
- MAP@K: Evaluates both relevance and ranking order of assessments

## Project Structure

```
recommendation_system/
├── data/                      # Assessment data files
├── models/                    # Recommender models
├── utils/                     # Utility modules for data processing, embeddings, etc.
├── streamlit_app/             # Streamlit web interface
│   └── app.py                 # Streamlit application
├── main.py                    # Main module with CLI interface
├── build_embeddings.py        # Script to build embeddings
├── evaluate_recommender.py    # Evaluation module
├── run_app.py                 # Script to run the Streamlit app
├── test_recommender.py        # Test script
└── requirements.txt           # Python dependencies
```
