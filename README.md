#Instructions for Configuring an Explorer Plug-in (App)

The explorer plugin operates on a single image service published from a composite band raster dataset in a File GeoDatabase on the server. The plugin creates slider bars or check boxes that draw their data from attributes in the rasters. When the user adjusts the slider values, they become weights that are multiplied by the values in the fields they correspond to, summed, then divided by the sum of the weights to produce a total score. The layer is then rendered using this score for the user to see.

Score = Sum ( weight * value) / Sum (weight)

To create an explorer plugin you must do three things.  

1. Publish your data.
2. Copy the code to the plugins directory for the site you are working with.
3. Configure the plugin. 

## Preparing and Publishing the Data

For each parameter, you must create a FGDBR raster with values from 0 (low suitability) to 40 (high suitability). For example, a raster might have three values 0 (low), 20 (medium), 40 (high). Each raster dataset should be an 8 bit, unsigned integer, 10 meter cell size, and projected to WGS 1984 Web Mercator Auxiliary Sphere.  Statistics should be built for each raster and the attribute tables should only have three fields, ObjectID, Value, and Count.       

Once you have your individual raster datasets, use the “Composite Bands” tool in ArcToolbox to create a single multi-band raster dataset.  Make sure you document the parameter that each band represents.  Place the composite band raster into the \\dev-services\data\crimageservices.gdb  located on the coastal resilience server 10.1.4.10.  

Once the data are loaded, right click on the raster and select “Share as Image Service” and follow the instructions to publish the service. When prompted, select “Publish Service to and Existing Folder” and choose “rasterExplorer” from the drop down menu.  

## Copy the Code and Configure the Plugin

Copy the required configuration files necessary for the Restoration Explorer from github (explorer.json, icon.png, icon_active.png, RestorationExplorer_c.jpg). Place these files in a folder titled “restoration_explorer” within the “plugins” folder for your region.  For each parameter, customize the code block to your data.

#### For example, 
 	{
		"default": 5,	<!--where the slider will be placed when the app is first opened -->
		"group": "all",     <!—all the parameters will be shown initially -->
		"index": "B1",	<!—the band within the image service that displays this parameter -->
		"max": 10,	<!—max weight a user can select -->
		"min": 0, 	<!—min weight a user can select -->
		"step": 1, 	<!—step between weights -->
		"text": "Depth Score",  <!—title of the parameter -->
		"help": "Depths < = 6 feet are more suitable for oysters in NC region.”, <!—help text-->
		"type": "layer"	<!--type-->
	},
	
Edit the last code block in the explorer.json file to point to your image service and customize the app legend as needed.

#### For example,
      "name": "Pamlico Sound, NC",	<!—The name shown in the app region drop down menu-- >
      "url": http://dev.services2.coastalresilience.org:6080/arcgis/rest/services/rasterExplorer/nc_restoration_explorer_10/ImageServer",			<!—The location of your image service -- >
      "methods": "methods/NC_Restoration_Explorer_Methods.pdf",	<!—the location of the methods document-- >
      "colorRamp": [[1, 255, 255, 129], [2, 204, 255, 51], [3, 76, 190, 110], [4, 13, 31, 133]], <!—the colors shown in the legend (first number is the value of the outputValues(see Below) the other three are the RGB values-- >
      "inputRanges" : [-255,9,10,19,20,29,30,255],	<!—Range of values for total suitability symbolized for each quartile in the legend. (<9 low; 10-19 low/med; 10-29 med/high; >30  high). -- >
      "outputValues" : [1,2,3,4]	<!—this legend will have four symbolized groups -- >
       
Lastly, add the restoration_explorer plugin to the plugin.json file for your region. 

#### For example,
   {
      "plugins": [
	      {
            "repo": "explorer",
            "name": "restoration_explorer"
         }
      ]
   }

Save, commit, and sync your changes to github.  If you have permissions to update the geosite-framework-build, do so.  If not, notify a Coastal Resilience data administrator to update the appropriate build (dev or production) so your changes are visible online. 


  
