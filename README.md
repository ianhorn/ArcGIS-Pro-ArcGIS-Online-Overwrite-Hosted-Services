# AGOL Workflow to Overwrite Hosted Services


The repo demonstrates how to use of [ArcPy](https://doc.esri.com/en/arcgis-pro/latest/arcpy/get-started/what-is-arcpy-.html) and the [ArcGIS API for Python](https://developers.arcgis.com/python/latest/) to overwrite existing hosted services.  

## Setup

#### Notebook

This Jupyter [Notebook](OverwriteHostedServices.ipynb) uses ArcGIS Pro's default Python environment.  You may clone the environment, but it is not necessary because the script requires no new packages.  

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
CLIENT_ID = "your_client_id_here"

DB_USER = "db_user"
DB_PASSWORD = "db_password"
INSTANCE = 'instance.awesome.workplace'
DATABASE = 'awesome_vectors'
DATABASE_PLATFORM = 'SQL_SERVER'
DB_CONNECTION_NAME = 'awesome_instance_awesome'
```