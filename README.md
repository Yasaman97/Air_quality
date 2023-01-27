# Predicting air quality index

Course: ID2223-Scalable Machine Learning and Deep Learning
Contributor:<a href="https://github.com/Yasaman97">Yasaman Pazhoolideh</a>

## About

This project aims to predict the API (Air Quality Index) for four cities, Paris, Nice, Copenhagen, and Helsinki.

## Data
The Air Quality data is from [World Air Quality Index](https://aqicn.org//here/). And, the weather data, is from [VisualCrossing](https://www.visualcrossing.com/).

It is necessary to create an `.env` configuration file with the API keys from these websites:
![](images/api_keys_env_file.png)


## Implementation
1. Backfill Features to the Feature Store,
2. Create a feature pipeline,
3. Create Feature views & Training Datasets,
4. Train a model and upload it to the Model Registry,
5. Deploy Streamlit app.
6. User Interface

### Feature Pipeline
The project uses historical data and new data. Two pipelines store these data on HopsworksData is ingested into [Hopsworks](https://www.hopsworks.ai/) Feature Store with the help of two main pipelines: one for historical data and one for fresh new data. The historical data is run once in a batch, and saves the air quality and weather data on Hopsworks. The second pipeline takes the new data everyday, and and each time adds a new row to the feature groups previously saved. Then, a Feature View is created by joining air quality and weather data.

### Training Pipeline
The training pipeline retrieves the Feature View and using trains on the data using the XGBboost model. The training pipeline runs every day. The model is then saved on Hopsworks. 

### Inference Pipeline
The inference pipeline retrieves the model and runs it everyday and saves the predictions.

### Streamlit app
To run streamlit app (after you have run all notebooks and already have required feature groups in Feature Store and model in Model Registry), simply type:

`python -m streamlit run streamlit_app.py` on Windows

or

`python3 -m streamlit run streamlit_app.py` on Unix

The cities the model was trained on can be viewed on the map, and by clicking on them, the data about them is shown, and a table on the side shows the predictions for API of those cities for the next day.

### User Interface
The User Interface shows the API predictions for the next 7 days.


Hugging Face space can be found [here](https://huggingface.co/spaces/Yasaman/air_quality).