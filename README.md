#Instructions for Configuring an Explorer Plug-in (App)

The explorer plugin operates on a single vector GIS layer in an enterprise GeoDatabase (e.g. PostGIS, MSSQL server etc.)  The plugin creates slider bars or check boxes that draw their data from fields in the attribute table for the vector layer.  When the user adjusts the slider values they become weights that are multiplied by the values in the fields they correspond with before they are added together to produce a total score.  The layer is then rendered using this score for the user to see.

To create an explorer plugin you must do three things.  

1. Publish your data.
2. Copy the code to the plugins directory for the site you are working with.
3. Configure the plugin. 

## Preparing and Publishing the Data

The data that you use should all be in one layer.  If your data is in multiple layers you should use an overlay function (Union or Intersect) to get your data into a single layer.  Identify which attributes from your layer will be used for the sliders).  Often it can reduce the size of your data if you dissolve your layer using ALL of the necessary attribute fields as the basis for your dissolve.

Once you have this single layer, you need to place this layer into an enterprise GIS database.  For coastal resilience there is already one set up for this purpose.  You can connect to this database in ArcCatalog by navigating to the database connections section and right clicking --> "Add Connection".  Then use the following information to connect:

* Database Platform: PostGreSQL
* Instance: 10.1.5.21
* Authentication Type: Database Authentication
* User name and password: (email Zach or George)
* Database: cr_postgres

If you end up using your own geodatabase keep track of the above as you will need it later (particularly Database and username).

   