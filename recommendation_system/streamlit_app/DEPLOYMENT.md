# Deploying to Streamlit Cloud

This guide will help you deploy the SHL Assessment Recommender to Streamlit Cloud.

## Option 1: Deploy the Standalone App (Recommended)

For the **simplest deployment** that doesn't rely on any other files:

1. Create a new app on [Streamlit Cloud](https://streamlit.io/cloud)
2. Connect to your GitHub repository
3. Set the Main app file path to:
   ```
   recommendation_system/streamlit_app/standalone_app.py
   ```
4. Add your OpenAI API key as a secret in the app settings:
   ```
   OPENAI_API_KEY = "your-actual-api-key"
   ```
5. Deploy!

This standalone app contains all the code needed to run the recommender with sample data directly in Streamlit Cloud, without needing any other files or dependencies.

## Option 2: Deploy the Full App (More Complex)

If you want to deploy the full app with all features:

1. Create a new app on [Streamlit Cloud](https://streamlit.io/cloud)
2. Connect to your GitHub repository
3. Set the Main app file path to:
   ```
   recommendation_system/streamlit_app/app.py
   ```
4. Add your OpenAI API key as a secret in the app settings:
   ```
   OPENAI_API_KEY = "your-actual-api-key"
   ```
5. Deployment may require additional configuration due to:
   - Python path issues
   - Dependency installation
   - Qdrant vector store initialization

## Troubleshooting

If you encounter any issues deploying:

1. Check the logs in Streamlit Cloud's app dashboard
2. Common errors:
   - **Module import errors**: Try using the standalone app instead
   - **Dependency errors**: Check if you need to update the requirements.txt file
   - **API key errors**: Make sure your OpenAI API key is correctly set in the secrets
   - **Path errors**: Try using absolute imports instead of relative imports

## Running Locally

To run the app locally:

```bash
cd recommendation_system
streamlit run streamlit_app/standalone_app.py
```

For the full app:

```bash
cd recommendation_system
python run_app.py
```
