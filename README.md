# ArcGIS Pro - AGOL Workflow to Overwrite Hosted Services


The repo demonstrates how to use [ArcPy](https://doc.esri.com/en/arcgis-pro/latest/arcpy/get-started/what-is-arcpy-.html) and the [ArcGIS API for Python](https://developers.arcgis.com/python/latest/) to overwrite existing hosted services to ArcGIS Online (AGOL). 

The objective of the notebook is to overwrite multiple hosted feature services.  You will need to gather your hosted services item ids and titles.  These values plus the values of your feature classes and output File Geodatabase names (e.g., Ky_Public_Schools_WM) are combined together as a Pandas DataFrame\*.

```python
mapping = {
  '<database.SCHEMA.feature_class>': ('<ITEM_ID>', '<ITEM_TITLE>','<FGDB_NAME'),
  '<database.SCHEMA.feature_class>': ('<ITEM_ID>', '<ITEM_TITLE>','<FGDB_NAME'),
  '<database.SCHEMA.feature_class>': ('<ITEM_ID>', '<ITEM_TITLE>','<FGDB_NAME')
}
```

\* *note: the notebook walks through a feature dataset to create the initial DataFrame*

## Setup

Feel free to fork or download this repo for your personal use.

#### Notebook

The Jupyter [Notebook](OverwriteHostedServices.ipynb) uses ArcGIS Pro's default Python environment.  You may clone the environment, but it is not necessary because the script requires no new packages.  

#### Credentials

As a best practice, AGOL credentials are setup to securely login. Checkout the API's documentation on [OAuth 2.0 authentication](https://developers.arcgis.com/documentation/security-and-authentication/user-authentication/) to set up your authentication.  

```python
# AGOL login. Will launch a browser window for OAuth2 authentication.
# Select the appropriate user account when prompted.
# Copy and paste the authentication token.

gis = GIS(url="https://wwww.arcgis.com", client_id=CLIENT_ID)
```

Alternatively, you can use environmental variables such as an `env.py` file.  Because ArcPy doesn't have the *dotenv* package to import varbiables, I set up a `creds.py` file and import the variables directly.

Sample creds.py file
```python
# CLient ID from AGOL Developer Credentials
CLIENT_ID = "your_client_id_here"

# Dabatabase variables
DB_USER = "db_user"
DB_PASSWORD = "db_password"
INSTANCE = 'instance.awesome.workplace'
DATABASE = 'awesome_vectors'
DATABASE_PLATFORM = 'SQL_SERVER'
DB_CONNECTION_NAME = 'awesome_instance_awesome'
```

## Troubleshooting 

Due to ArcGIS Pro's reliably unreliable behavior, you can expect to run into the infamous `Error 999999`.  If this happens:
1. Shutdown the ArcGIS Pro Desktop Application
2. Open Task Managar
3. Kill any lingering ArcGIS Pro background processes
4. Open Pro
5. Run notebook

The notebook can be executed in ArcGIS Pro or in your preferred text editor like VS Code.  Just make sure you point the IDE the python environment, most likely 

