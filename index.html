
//Objective : to analyze and map out the flood extent and pattern of lower Saxony between Dec 2023 and Jan 2024.
//by taking time series data and computing the flood extent in each date. 

//Load shapefile of region of interest (roi)

Map.addLayer(roi);
Map.centerObject(roi, 7);

var collection = ee.ImageCollection("COPERNICUS/S1_GRD")
   .filter(ee.Filter.eq('instrumentMode', 'IW')) 
   .filter(ee.Filter.eq('orbitProperties_pass', 'DESCENDING'))
   .filterMetadata('resolution_meters', 'equals' , 10)
   .filterDate('2023-12-14', '2024-01-22')
   .filterBounds(roi);
print(collection, 'Sentinel-1 Collection');
var collection_list=ee.ImageCollection(collection).toList(100);

//selecting the available images on each date from the list clip and Mosaic

var image1 = ee.Image(ee.List(collection_list).get(0)).clip(roi);  
var image2 = ee.Image(ee.List(collection_list).get(1)).clip(roi);  
var image3 = ee.Image(ee.List(collection_list).get(2)).clip(roi);  
var Dec_15 = ee.ImageCollection([image1, image2, image3]).mosaic();

var image9 = ee.Image(ee.List(collection_list).get(8)).clip(roi);  
var image10 = ee.Image(ee.List(collection_list).get(9)).clip(roi);  
var image11 = ee.Image(ee.List(collection_list).get(10)).clip(roi);  
var Dec_27 = ee.ImageCollection([image9, image10, image11]).mosaic();

var image17 = ee.Image(ee.List(collection_list).get(16)).clip(roi);  
var image18 = ee.Image(ee.List(collection_list).get(17)).clip(roi); 
var image19 = ee.Image(ee.List(collection_list).get(18)).clip(roi); 
var Jan_08 = ee.ImageCollection([image17, image18, image19]).mosaic();

var image25 = ee.Image(ee.List(collection_list).get(24)).clip(roi); 
var image26 = ee.Image(ee.List(collection_list).get(25)).clip(roi); 
var image27 = ee.Image(ee.List(collection_list).get(26)).clip(roi); 
var Jan_20 = ee.ImageCollection([image25, image26, image27]).mosaic();

//Select the VH band from the mosaic image 
//VH is a better polarization to detect inundation cuased by open water because the signal doesn not depolarize(low backscatter)

Map.centerObject(roi, 7);
Map.addLayer(Dec_15.select('VH'), {min:-25, max:-5}, 'S1 Dec. 15, 2023 VH', 0);
Map.addLayer(Dec_27.select('VH'), {min:-25, max:-5}, 'S1 Dec. 27, 2023 VH', 0);
Map.addLayer(Jan_08.select('VH'), {min:-25, max:-5}, 'S1 Jan. 08, 2024 VH', 0);
Map.addLayer(Jan_20.select('VH'), {min:-25, max:-5}, 'S1 Jan. 20, 2024 VH', 0);

//Create RGB to see the changes in a colorful way (Red/green/blue means the backscatter is relatively high, it is not flooded
//Pick is an indication of flooding: High in the Red and Blue Channel, Source: NASA

var composite1 = Dec_15.select('VH').addBands(Dec_27.select('VH')).addBands(Jan_08.select('VH'));
var composite2 = Dec_27.select('VH').addBands(Jan_08.select('VH')).addBands(Jan_20.select('VH'));

Map.addLayer(composite1, {min: -25, max: -5}, 'Dec15(R)/Dec27(G)/Jan08(B) VH', 0);
Map.addLayer(composite2, {min: -25, max: -5}, 'Dec27(R)/Jan08(G)/Jan20(B) VH', 0);


//Apply a spatial speckle filter (Speckle is granular noise that inherently exists on the image and degrade the quality of the image.
//(grainy) i.e. salt and peper texture of the image resulted from multiple scattering returns within each resolution cell)

var SMOOTHING_RADIUS = 50; //As the smoothing value increase the greater the reduction of speckle but the higher reduction in spatial resolution.
var Dec_15_filt = Dec_15.focal_mean(SMOOTHING_RADIUS, 'circle', 'meters');
var Dec_27_filt = Dec_27.focal_mean(SMOOTHING_RADIUS, 'circle', 'meters');
var Jan_08_filt = Jan_08.focal_mean(SMOOTHING_RADIUS, 'circle', 'meters');
var Jan_20_filt = Jan_20.focal_mean(SMOOTHING_RADIUS, 'circle', 'meters');

//Display filtered images

Map.addLayer(Dec_15_filt, {min:-25,max:-5}, 'FilteredVH_Dec_15',0);
Map.addLayer(Dec_27_filt, {min:-25,max:-5}, 'FilteredVH_Dec_27',0);
Map.addLayer(Jan_08_filt, {min:-15,max:-5}, 'FilteredVH_Jan_08',0);
Map.addLayer(Jan_20_filt, {min:-15,max:-5}, 'FilteredVH_Jan_20',0);

//Create difference images for the respective dates
//In order to substract logarithmic values (dB) it is imperaive to perform a division (subtracting from the after image before)
//dB measure the loudness of a sound, indiacte how loud a sound is relative to some reference, representated in units of 
//micropascals)

var Dec_15_Dec_27_diff= Dec_27_filt.select('VH').divide(Dec_15_filt.select('VH'));
var Dec_27_Jan_08_diff= Jan_08_filt.select('VH').divide(Dec_27_filt.select('VH'));
var Dec_15_Jan_20_diff= Jan_20_filt.select('VH').divide(Dec_15_filt.select('VH'));

Map.addLayer(Dec_15_Dec_27_diff, {min: 0,max:2}, 'Difference VH filtered_Dec15_Dec27', 0);//the brighter values are where there is inundation 
Map.addLayer(Dec_27_Jan_08_diff, {min: 0,max:2}, 'Difference VH filtered_Dec27_Jan08', 0);
Map.addLayer(Dec_15_Jan_20_diff, {min: 0,max:2}, 'Difference VH filtered_Dec15_Jan20', 0);

// Apply a adaptive threshold - based on the difference image values; 

var UPPER_THRESHOLD = 1.25; //a value greater than the threshold value is considered as inundation 
var inundation_Dec_15_Dec_27 = Dec_15_Dec_27_diff.gt(UPPER_THRESHOLD);
var inundation_Dec_27_Jan_08 = Dec_27_Jan_08_diff.gt(UPPER_THRESHOLD);
var inundation_Dec_15_Jan_20 = Dec_15_Jan_20_diff.gt(UPPER_THRESHOLD);

Map.addLayer(inundation_Dec_15_Dec_27.updateMask(inundation_Dec_15_Dec_27),
{palette:"070908"},'Flood_Map Dec27(TH) - Black',0);

Map.addLayer(inundation_Dec_27_Jan_08.updateMask(inundation_Dec_27_Jan_08),
{palette:"#ff4710"},'Flood_Map Jan08(TH) - Red',0);

Map.addLayer(inundation_Dec_15_Jan_20.updateMask(inundation_Dec_15_Jan_20),
{palette:"#ffbc3d"},'Flood_Map Jan20(TH) - Yellow',0);

// A. The next step is to refine the Flood Map Using Pixel connectivity, 
//remove those connected by 20 pixels or less considered as a noise 

var connections = inundation_Dec_15_Dec_27.connectedPixelCount();    
var inundation2_Dec_15_Dec_27 = inundation_Dec_15_Dec_27.updateMask(connections.gte(20));

var connections = inundation_Dec_27_Jan_08.connectedPixelCount();    
var inundation2_Dec_27_Jan_08 = inundation_Dec_27_Jan_08.updateMask(connections.gte(20));

var connections = inundation_Dec_15_Jan_20.connectedPixelCount();    
var inundation2_Dec_15_Jan_20 = inundation_Dec_15_Jan_20.updateMask(connections.gte(20));


Map.addLayer(inundation2_Dec_15_Dec_27.updateMask(inundation2_Dec_15_Dec_27),
{palette:"#0f28ee"},'Flooding_PC Dec. 27 - Blue',0);

Map.addLayer(inundation2_Dec_27_Jan_08.updateMask(inundation2_Dec_27_Jan_08),
{palette:"#0f28ee"},'Flooding_PC Jan. 08 - Blue',0);

Map.addLayer(inundation2_Dec_15_Jan_20.updateMask(inundation2_Dec_15_Jan_20),
{palette:"#0f28ee"},'Flooding_PC Jan. 20 - Blue',0);

// B. Remove misclassified pixels in areas where the slope is greater than 5% using SRTM-DEM
// Slope class less than 5%, can be maintained, while above 5% eliminated.  

var srtm = ee.Image("USGS/SRTMGL1_003");
var terrain = ee.Algorithms.Terrain(srtm);
var slope = terrain.select('slope');
var inundation3_Dec_15_Dec_27 = inundation2_Dec_15_Dec_27.updateMask(slope.lt(5));
var inundation3_Dec_27_Jan_08 = inundation2_Dec_27_Jan_08.updateMask(slope.lt(5));
var inundation3_Dec_15_Jan_20 = inundation2_Dec_15_Jan_20.updateMask(slope.lt(5));

//Map.addLayer(srtm, {min:0,max:300}, 'SRTM', 0);

Map.addLayer(inundation3_Dec_15_Dec_27.updateMask(inundation3_Dec_15_Dec_27),
{palette:"#ec3621"},'Flooding Dec. 27 - Red_after_slope',0);

Map.addLayer(inundation3_Dec_27_Jan_08.updateMask(inundation3_Dec_27_Jan_08),
{palette:"#ec3621"},'Flooding Jan. 08 - Red_after_slope',0);

Map.addLayer(inundation3_Dec_15_Jan_20.updateMask(inundation3_Dec_15_Jan_20),
{palette:"#ec3621"},'Flooding Jan. 20 - Red_after_slope',0);

// C. Remove misclassified pixels in areas where there is pernament open water using Copernicus Global Land Service (CGLS) land cover map (100m)

var global_landcover = ee.Image("COPERNICUS/Landcover/100m/Proba-V-C3/Global/2019").select('discrete_classification');
var landcover_roi = global_landcover.clip(roi);

// Extract only water pixels from CGLS using class value equal to 80 (Permanent water bodies) or 200 (Oceans, seas).  
// Extract only water pixels from CGLS using class value equal to 80 or 200
//var water = landcover.eq(80,200);

var water = landcover_roi.eq(80).or(landcover_roi.eq(200));
var watermask = inundation3_Dec_15_Dec_27.where(water, 0);
var inundation4_Dec_15_Dec_27 = watermask.updateMask(watermask);
var watermask = inundation3_Dec_27_Jan_08.where(water, 0);
var inundation4_Dec_27_Jan_08 = watermask.updateMask(watermask);
var watermask = inundation3_Dec_15_Jan_20.where(water, 0);
var inundation4_Dec_15_Jan_20 = watermask.updateMask(watermask);


Map.addLayer(inundation4_Dec_15_Dec_27.updateMask(inundation4_Dec_15_Dec_27),
{palette:"22ec3b"},'Final_Flood Extent Map Dec. 27 - Green',1);

Map.addLayer(inundation4_Dec_27_Jan_08.updateMask(inundation4_Dec_27_Jan_08),
{palette:"ecda02"},'Final_Flood Extent Map Jan. 08 - Yellow',1);

Map.addLayer(inundation4_Dec_15_Jan_20.updateMask(inundation4_Dec_15_Jan_20),
{palette:"ffa927"},'Final_Flood Extent Map Jan. 20 - Orange',1);

//Map.addLayer(landcover_roi, {}, "Land Cover", 0);

//.................End...........................................
// Calculate inundation extent for each date, Dec_27

var inundation_area_Dec_27 = inundation4_Dec_15_Dec_27.multiply(ee.Image.pixelArea());

//Sum the area covered by inundated pixels for Dec_27 

var inundation_stats_Dec_27 = inundation_area_Dec_27.reduceRegion({
  reducer: ee.Reducer.sum(),              
  geometry: roi,
  scale: 10, // Sentinel-1 Resolution
  maxPixels: 1e9,
  bestEffort: false
  });

// Convert inundated extent to hectares for Dec_27

var inundation_area_ha_Dec_27 = inundation_stats_Dec_27.getNumber("VH").divide(10000).round(); 
print(inundation_area_ha_Dec_27, 'Hectares of Inundated Area for Dec. 27'); 

//Sum the area covered by inundated pixels for Jan_08 

var inundation_area_Jan_08 = inundation4_Dec_27_Jan_08.multiply(ee.Image.pixelArea());

var inundation_stats_Jan_08 = inundation_area_Jan_08.reduceRegion({
  reducer: ee.Reducer.sum(),              
  geometry: roi,
  scale: 10, // Sentinel-1 Resolution
  maxPixels: 1e9,
  bestEffort: false
  });
 
// Convert inundated extent to hectares for Jan_08 

var inundation_area_ha_Jan_08 = inundation_stats_Jan_08.getNumber("VH").divide(10000).round(); 
print(inundation_area_ha_Jan_08, 'Hectares of Inundated Area for Jan. 08'); 

//Calculate inundation extent for Jan 20

var inundation_area_Jan_20 = inundation4_Dec_15_Jan_20.multiply(ee.Image.pixelArea());

// Sum the area covered by inundated pixels for Jan_20 

var inundation_stats_Jan_20 = inundation_area_Jan_20.reduceRegion({
 reducer: ee.Reducer.sum(),              
 geometry: roi,
 scale: 10, // Sentinel-1 Resolution
 maxPixels: 1e9,
 bestEffort: false
 });
  
// Convert inundated extent to hectares for Jan_20 

var inundation_area_ha_Jan_20 = inundation_stats_Jan_20.getNumber("VH").divide(10000).round(); 
print(inundation_area_ha_Jan_20, 'Hectares of Inundated Area for Jan. 20'); 

//........Calculate Flooded Agriculture land.......................................
// Copernicus Global Land Service (CGLS) land cover (100m) map to identify agricultural
// Extract only agricultural pixels from the CGLS. The agricultural class value is equal to 40

var agriculture = landcover_roi.eq(40);
var agriculturemask = landcover_roi.updateMask(agriculture);

// Calculate the affected agricultural using the flood layer for Dec 27 

var agriculture_affected_Dec_27 = inundation4_Dec_15_Dec_27.updateMask(agriculturemask);

// Calculate the pixel area where there are agricultural and it is flooded for Dec 27

var agriculture_pixelarea = agriculture_affected_Dec_27.multiply(ee.Image.pixelArea()); 

// Sum pixels of affected agricultural layer

var agriculture_stats = agriculture_pixelarea.reduceRegion({
 reducer: ee.Reducer.sum(), //sum all pixels with area information                
 geometry: roi,
 scale: 10,
 maxPixels: 1e9
 });
 
// Convert area to hectares for Dec 27

var agriculture_area_ha_Dec_27 = agriculture_stats.getNumber("VH").divide(10000).round();

// Calculate the affected agricultural using the flood layer for Jan 08

var agriculture_affected_Jan_08 = inundation4_Dec_27_Jan_08.updateMask(agriculturemask);

// Calculate the pixel area where there are agricultural and it is flooded for Jan 08

var agriculture_pixelarea = agriculture_affected_Jan_08.multiply(ee.Image.pixelArea()); 

// Sum pixels of affected agricultural layer

var agriculture_stats = agriculture_pixelarea.reduceRegion({
 reducer: ee.Reducer.sum(), //sum all pixels with area information                
 geometry: roi,
 scale: 10,
 maxPixels: 1e9
 });
 
// Convert area to hectares for Jan 08

var agriculture_area_ha_Jan_08 = agriculture_stats.getNumber("VH").divide(10000).round();

// Calculate the affected agricultural using the flood layer for Jan 20

var agriculture_affected_Jan_20 = inundation4_Dec_15_Jan_20.updateMask(agriculturemask);

// Calculate the pixel area where there are agricultural and it is flooded for Jan 20

var agriculture_pixelarea = agriculture_affected_Jan_20.multiply(ee.Image.pixelArea()); 

// Sum pixels of affected agricultural layer

var agriculture_stats = agriculture_pixelarea.reduceRegion({
 reducer: ee.Reducer.sum(), //sum all pixels with area information                
 geometry: roi,
 scale: 10,
 maxPixels: 1e9
 });
 
// Convert area to hectares for Jan 20

var agriculture_area_ha_Jan_20 = agriculture_stats.getNumber("VH").divide(10000).round();

// Print results 

print (agriculture_area_ha_Dec_27, 'Hectares of Inundated agriculture on Dec. 27');
print (agriculture_area_ha_Jan_08, 'Hectares of Inundated agriculture on Jan. 08');
print (agriculture_area_ha_Jan_20, 'Hectares of Inundated agriculture on Jan. 20');

// Add crop layer to map

Map.addLayer(agriculturemask, {}, 'Agriculture', 0);

// Add flooded crop area to map

Map.addLayer(agriculture_affected_Dec_27, {palette:"22ec3b"}, 'Flooded agriculture on Dec. 27 - Green', 0);
Map.addLayer(agriculture_affected_Jan_08, {palette:"ecda02"}, 'Flooded agriculture on Jan. 08 - Yellow', 0);
Map.addLayer(agriculture_affected_Jan_20, {palette:"#ff3925"}, 'Flooded agriculture on Jan. 20 - Red', 0);


//.................................... Calculate Built-up area.......................................
// Extract only urban pixels from the CGLS. The built-up class value is equal to 50

var Urban = landcover_roi.eq(50);
var Urbanmask = landcover_roi.updateMask(Urban);

// Calculate the affected built-up using the flood layer for Dec 27 

var Urban_affected_Dec_27 = inundation4_Dec_15_Dec_27.updateMask(Urbanmask);

// Calculate the pixel area where there are built-up and it is flooded for Dec 27

var Urban_pixelarea = Urban_affected_Dec_27.multiply(ee.Image.pixelArea()); 

// Sum pixels of affected built-up layer

var Urban_stats =  Urban_pixelarea.reduceRegion({
 reducer: ee.Reducer.sum(), //sum all pixels with area information                
 geometry: roi,
 scale: 10,
 maxPixels: 1e9
 });
 
// Convert area to hectares for Dec 27

var Urban_area_ha_Dec_27 = Urban_stats.getNumber("VH").divide(10000).round();

// Calculate the affected built-up using the flood layer for Jan 08

var Urban_affected_Jan_08 = inundation4_Dec_27_Jan_08.updateMask(Urbanmask);

// Calculate the pixel area where there are Urabn and it is flooded for Jan 08

var Urban_pixelarea = Urban_affected_Jan_08.multiply(ee.Image.pixelArea()); 

// Sum pixels of affected Urban layer

var Urban_stats = Urban_pixelarea.reduceRegion({
 reducer: ee.Reducer.sum(), //sum all pixels with area information                
 geometry: roi,
 scale: 10,
 maxPixels: 1e9
 });
 
// Convert area to hectares for Jan 08

var Urban_area_ha_Jan_08 = Urban_stats.getNumber("VH").divide(10000).round();

// Calculate the affected Urban using the flood layer for Jan 20

var Urban_affected_Jan_20 = inundation4_Dec_15_Jan_20.updateMask(Urbanmask);

// Calculate the pixel area where there are Urban and it is flooded for Jan 20
var Urban_pixelarea = Urban_affected_Jan_20.multiply(ee.Image.pixelArea()); 

// Sum pixels of affected Urban layer

var Urban_stats = Urban_pixelarea.reduceRegion({
 reducer: ee.Reducer.sum(), //sum all pixels with area information                
 geometry: roi,
 scale: 10,
 maxPixels: 1e9
 });

// Convert area to hectares for Jan 20
var Urban_area_ha_Jan_20 = Urban_stats.getNumber("VH").divide(10000).round();

// Print results 
print (Urban_area_ha_Dec_27, 'Hectares of Inundated Urban on Dec. 27');
print (Urban_area_ha_Jan_08, 'Hectares of Inundated Urban on Jan. 08');
print (Urban_area_ha_Jan_20, 'Hectares of Inundated Urban on Jan. 20');

// Add crop layer to map
Map.addLayer(Urbanmask, {}, 'Urban', 0);

// Add flooded Urban area to map
Map.addLayer(Urban_affected_Dec_27, {palette:"22ec3b"}, 'Flooded Urban on Dec. 27 - Green', 0);
Map.addLayer(Urban_affected_Jan_08, {palette:"ecda02"}, 'Flooded Urban on Jan. 08 - Yellow', 0);
Map.addLayer(Urban_affected_Jan_20, {palette:"#2245ff"}, 'Flooded Urban on Jan. 20 - Blue', 0);

/////////////////////////////////++++++++++++Create a Legend++++++++++++////////////

// set position of panel
var legend = ui.Panel({
  style: {
    position: 'bottom-right',
    padding: '8px 15px',
  }
});
 
// Create legend title
var titleTextVis = {
  'margin':'0px 0px 15px 0px',
  'fontSize': '18px', 
  'font-weight':'', 
  'color': '3333ff'
  };

var legendTitle = ui.Label('Flood Extent',titleTextVis);
 
// Add the title to the panel
legend.add(legendTitle);
 
// Create and modify the style for 1 row of the legend.
var makeRow = function(color, name) {
 
      // Create the label that is actually the colored box.
      var colorBox = ui.Label({
        style: {
          backgroundColor: color,
          // padding gives the box height and width.
          padding: '8px',
          margin: '0 0 4px 0'
        }
      });
 
      // Create the label the following description
      var description = ui.Label({
        value: name,
        style: {margin: '0 0 4px 6px'}
      });
 
      // return the panel
      return ui.Panel({
        widgets: [colorBox, description],
        layout: ui.Panel.Layout.Flow('horizontal')
      });
};
 
//  Palette with the colors
var palette =['#22ec3b', '#ecda02', 'ffa927'];
 
// description for each box
var names = ['Dec. 27','Jan. 08','Jan. 20'];
 
// Add color and and names
for (var i = 0; i < 3; i++) {
  legend.add(makeRow(palette[i], names[i]));
  }  

// add the legend to the map (you can also print the legend to the console)
Map.add(legend);


/////////////////////++++++++++++Create a description of your results++++++++++++///////////////////

// This sets the position where the panel will be displayed 
var results = ui.Panel({
  style: {
    position: 'bottom-left',
    padding: '8px 15px',
    width: '350px'
  }
});

// Set the visualtization parameters of the labels 
var textVis = {
  'margin':'0px 8px 2px 0px',
  'fontWeight':'bold'
  };
var numberVIS = {
  'margin':'0px 0px 15px 0px', 
  'color':'bf0f19',
  'fontWeight':'bold'
  };
var subTextVis = {
  'margin':'0px 0px 2px 0px',
  'fontSize':'12px',
  'color':'grey'
  };

var titleTextVis = {
  'margin':'0px 0px 15px 0px',
  'fontSize': '18px', 
  'font-weight':'', 
  'color': '3333ff'
  };

// Create lables for each of the results 
var title = ui.Label('Results', titleTextVis);

// Print flood extent 
var text1 = ui.Label('Estimated flood extent for North-west Saxony, Germany in 2024:',textVis);
var text1_2 = ui.Label ('using Sentinel-1 data from 2023-012-14 to 2024-01-22', subTextVis);
var number1 = ui.Label('Please wait...',numberVIS); 
inundation_area_ha_Dec_27.evaluate(function(val){number1.setValue(val+' hectares on Dec. 27')}),numberVIS;
var number1_2 = ui.Label('Please wait...',numberVIS); 
inundation_area_ha_Jan_08.evaluate(function(val){number1_2.setValue(val+' hectares on Jan. 08')}),numberVIS;
var number1_3 = ui.Label('Please wait...',numberVIS); 
inundation_area_ha_Jan_20.evaluate(function(val){number1_3.setValue(val+' hectares on Jan. 20')}),numberVIS;

// Print affected Agricultural
var text2 = ui.Label('Estimated flooded agricuture:',textVis);
var text2_2 = ui.Label('based on the CGLS landcover map', subTextVis);
var number2 = ui.Label('Please wait...',numberVIS);
agriculture_area_ha_Dec_27.evaluate(function(val){number2.setValue(val+' hectares on Dec. 27')}),numberVIS;
var number2_2 = ui.Label('Please wait...',numberVIS);
agriculture_area_ha_Jan_08.evaluate(function(val){number2_2.setValue(val+' hectares on Jan. 08')}),numberVIS;
var number2_3 = ui.Label('Please wait...',numberVIS);
agriculture_area_ha_Jan_20.evaluate(function(val){number2_3.setValue(val+' hectares on Jan. 20')}),numberVIS;

// Print affected built-up 
var text3 = ui.Label('Estimated flooded Urban:',textVis);
var text3_3 = ui.Label('based on the CGLS landcover map', subTextVis);
var number3 = ui.Label('Please wait...',numberVIS);
Urban_area_ha_Dec_27.evaluate(function(val){number2.setValue(val+' hectares on Dec. 27')}),numberVIS;
var number3_3 = ui.Label('Please wait...',numberVIS);
Urban_area_ha_Jan_08.evaluate(function(val){number2_2.setValue(val+' hectares on Jan. 08')}),numberVIS;
var number2_4 = ui.Label('Please wait...',numberVIS);
Urban_area_ha_Jan_20.evaluate(function(val){number2_3.setValue(val+' hectares on Jan. 20')}),numberVIS;

// Disclaimer
var text3 = ui.Label('Note- This is a demo product only. It has not been validated. Parts of this code were adapted from a UN-SPIDER December 2019 flooding script.',subTextVis);

// Add the labels to the panel 
results.add(ui.Panel([
        title,
        text1,
        text1_2,
        number1,
        number1_2,
        number1_3,
        text2,
        text2_2,
        number2,
        number2_2,
        number2_3,
        text3,
        text3_3,
        number3,
        number3_3,]
      ));

// Add the panel to the map 
Map.add(results);

//////////////////////////////////++++++++++++Export your results++++++++++++///////////
// Export Dec. 27 flooded area as a TIFF file 

//Difference image


Export.image.toDrive({
  image: composite1,  
  description: 'False_color_Dec/15/27/Jan/08',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
  });

Export.image.toDrive({
  image: composite2,  
  description: 'Dec27/Jan08(G)/Jan20(B)',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
  });

Export.image.toDrive({
  image: Dec_15_Dec_27_diff,  
  description: 'Diff_Dec_15_27',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
  });

Export.image.toDrive({
  image: Dec_27_Jan_08_diff,  
  description: 'Diff_Dec_27_Jan_08',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
  });

Export.image.toDrive({
  image: Dec_15_Jan_20_diff,  
  description: 'Diff_Dec_15_Jan_20',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
  });

Export.image.toDrive({
  image: inundation4_Dec_15_Dec_27,  
  description: 'Flood_extent_Dec27',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
  });

//Export SAR images of the respective dates 
Export.image.toDrive({
  image: Dec_15.select('VH'),  
  description: 'S1_Dec_15_VH',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
  });

Export.image.toDrive({
  image: Dec_27.select('VH'),  
  description: 'S1_Dec_27_VH',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
  });
  
Export.image.toDrive({
  image: Jan_08.select('VH'),  
  description: 'S1_Jan_08_VH',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
  });

Export.image.toDrive({
  image: Jan_20.select('VH'),  
  description: 'S1_Jan_20_VH',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
  });

///////////////////////////////////
//Export Agricultural and urban mask

var agricultureVectors = agriculturemask.reduceToVectors({
  scale: 10,
  geometryType:'polygon',
  geometry: roi,
  eightConnected: false,
  bestEffort:true,
  tileScale:2,
});

// Export your flood polygons to a shapefile
Export.table.toDrive({
  collection: agricultureVectors,
  description:'AgricultureVectors',
  fileFormat:'SHP',
  fileNamePrefix:'AgricultureVectors'
});

var UrbanVectors = Urbanmask.reduceToVectors({
  scale: 10,
  geometryType:'polygon',
  geometry: roi,
  eightConnected: false,
  bestEffort:true,
  tileScale:2,
});

// Export your flood polygons to a shapefile
Export.table.toDrive({
  collection: UrbanVectors,
  description:'UrbanVectors',
  fileFormat:'SHP',
  fileNamePrefix:'UrbanVectors'
});

// Export agricultural Dec27
Export.image.toDrive({
  image: agriculture_affected_Dec_27,  
  description: 'agriculture_affected_Dec_27',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
  });

// Export agricultural Jan08
Export.image.toDrive({
  image: agriculture_affected_Jan_08,  
  description: 'agriculture_affected_Jan_08',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
  });
  
// Export agricultural Jan20
Export.image.toDrive({
  image: agriculture_affected_Jan_20,  
  description: 'agriculture_affected_Jan_20',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
  });


// Export urban flood extent Dec27, Jan08, Jan20
Export.image.toDrive({
  image: Urban_affected_Dec_27,  
  description: 'Urban_affected_Dec_27',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
  });

Export.image.toDrive({
  image: Urban_affected_Jan_08,  
  description: 'Urban_affected_Jan_08',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
  }); 
  
Export.image.toDrive({
  image: Urban_affected_Jan_20,  
  description: 'Urban_affected_Jan_20',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
  }); 
  
// First convert your flood raster to polygons
var inundation4_Dec_15_Dec_27_vec = inundation4_Dec_15_Dec_27.reduceToVectors({
  scale: 10,
  geometryType:'polygon',
  geometry: roi,
  eightConnected: false,
  bestEffort:true,
  tileScale:2,
});


// Export your flood polygons to a shapefile
Export.table.toDrive({
  collection:inundation4_Dec_15_Dec_27_vec,
  description:'Flood_extent_Dec_27_vector',
  fileFormat:'SHP',
  fileNamePrefix:'flooded27_vec'
});



//....Jan 08
Export.image.toDrive({
  image: inundation4_Dec_27_Jan_08, 
  description: 'Flood_extent_Jan08',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
  //crs: "EPSG: 4326"
});

// Export flooded area as a shapefile
// First convert your flood raster to polygons
var inundation4_Dec_27_Jan_08_vec = inundation4_Dec_27_Jan_08.reduceToVectors({
  scale: 10,
  geometryType:'polygon',
  geometry: roi,
  eightConnected: false,
  bestEffort:true,
  tileScale:2,
});

// Export your flood polygons to a shapefile
Export.table.toDrive({
  collection:inundation4_Dec_27_Jan_08_vec,
  description:'Flood_extent_Jan_08_vector',
  fileFormat:'SHP',
  fileNamePrefix:'floodedJan08_vec'
});

//....Jan 20
Export.image.toDrive({
  image: inundation4_Dec_15_Jan_20, 
  description: 'Flood_extent_Jan20',
  scale: 30,
  region: roi,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e13,
});

// Export flooded area as a shapefile
// First convert your flood raster to polygons
var inundation4_Dec_15_Jan_20_vec = inundation4_Dec_15_Jan_20.reduceToVectors({
  scale: 10,
  geometryType:'polygon',
  geometry: roi,
  eightConnected: false,
  bestEffort:true,
  tileScale:2,
});

// Export your flood polygons to a shapefile
Export.table.toDrive({
  collection:inundation4_Dec_15_Jan_20_vec,
  description:'Flood_extent_Jan_20_vector',
  fileFormat:'SHP',
  fileNamePrefix:'floodedJan20_vec'
});




