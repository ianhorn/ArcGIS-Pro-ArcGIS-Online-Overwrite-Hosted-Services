# ArcGIS Pro - AGOL Workflow to Overwrite Hosted Services


The repo demonstrates how to use [ArcPy](https://doc.esri.com/en/arcgis-pro/latest/arcpy/get-started/what-is-arcpy-.html) and the [ArcGIS API for Python](https://developers.arcgis.com/python/latest/) to overwrite existing hosted services to ArcGIS Online (AGOL). 

#### Assumptions

The Hosted Service exists and was published via a script or upload of a file of spatial data format(e.g., File Geodataformat, GeoPackage, GeoJSON, etc.).  In other words, you services were not created using the ArcGIS Pro desktop application via share/publish.  

## Setup 

#### ArcGIS Pro

1. [Download Repo](https://github.com/ianhorn/ArcGIS-Pro-ArcGIS-Online-Overwrite-Hosted-Services/archive/refs/heads/main.zip)
2. Unzip locally
3. Copy *creds.py*, *creds_example.py*, and *OverwriteHostedServices.ipynb* into the root of your ArcGIS Pro project folder
4. Update *creds.py* using *creds_example.py* as a template.
5. Open Notebook in Pro
6. Follow instructions from [Notebook](#notebook)

#### VS Code (optional)

Feel free to fork or download this repo for your personal use.
```cmd
mkdir agol-overwrite-repo
cd agol-overwrite-repo
git clone https://github.com/ianhorn/ArcGIS-Pro-ArcGIS-Online-Overwrite-Hosted-Services.git .

git checkout -b mybranch
conda activate "C:\Program Files\ArcGIS\Pro\bin\Python\envs\arcgispro-py3"
```
1. Copy the content in the [creds_example.py](creds_example.py) file and paste in the the [creds.py](creds.py) file. 
2. Update variable values
3. Follow [Notebook](#notebook) instructions.

## Notebook

The Jupyter [Notebook](OverwriteHostedServices.ipynb) uses ArcGIS Pro's default Python environment.  You may clone the environment, but it is not necessary because the script requires no new packages.  

The objective of the notebook is to overwrite multiple hosted feature services.  You will need to gather your hosted services item ids and titles.  These values plus the values of your feature classes and output File Geodatabase names (e.g., Ky_Public_Schools_WM) are combined together as a Pandas DataFrame\*.

```python
mapping = {
  '<database.SCHEMA.feature_class>': ('<ITEM_ID>', '<ITEM_TITLE>','<FGDB_NAME'),
  '<database.SCHEMA.feature_class>': ('<ITEM_ID>', '<ITEM_TITLE>','<FGDB_NAME'),
  '<database.SCHEMA.feature_class>': ('<ITEM_ID>', '<ITEM_TITLE>','<FGDB_NAME')
}
```

The arcpy environment variables set set to `ovarcpy.env.overwriteOutput = True` and    
`arcpy.env.addOutputsToMap = False`.  Not loading output to the projects map or scene prevents any lock creation.


\* *note: the notebook walks through a feature dataset to create the initial DataFrame*

## Credentials

As a best practice, AGOL credentials are setup to securely login. Checkout the API's documentation on [OAuth 2.0 authentication](https://developers.arcgis.com/documentation/security-and-authentication/user-authentication/) to set up your authentication.  


>AGOL login: running this cell launches a browser window for OAuth2 authentication.  
Select the appropriate user account when prompted.  
Copy and paste the authentication token.  

Or, replace `client_id=CLIENT_ID` with `username=<USERNAME>, password=<PASSWORD>` -  ot recommended
```python
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

Due to ArcGIS Pro's reliably unreliable behavior, you can expect to run into the infamous *`Error 999999`* occasionally.  If this happens:
1. Shutdown the ArcGIS Pro Desktop Application
2. Open Task Managar
3. Kill any lingering ArcGIS Pro background processes
4. Open Pro
5. Run notebook

The notebook can be executed in ArcGIS Pro or in your preferred text editor like VS Code.  Just make sure you point the IDE the python environment, most likely `C:\Program Files\ArcGIS\Pro\bin\Python\envs\arcgispro-py3\python.exe`.

