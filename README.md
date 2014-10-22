#Instructions for Configuring an Explorer Plug-in (App)

The explorer plugin operates on a single vector GIS layer in an enterprise GeoDatabase (e.g. PostGIS, MSSQL server etc.)  The plugin creates slider bars or check boxes that draw their data from fields in the attribute table for the vector layer.  When the user adjusts the slider values they become weights that are multiplied by the values in the fields they correspond with before they are added together to produce a total score.  The layer is then rendered using this score for the user to see.

To create an explorer plugin you must do three things.  

1. Publish your data.
2. Copy the code to the plugins directory for the site you are working with.
3. Configure the plugin. 