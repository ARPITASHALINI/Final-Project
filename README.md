# Working with Folium to make interactive point and polyline maps. 

This tutorial was created as a final project submission for the course IDCE 30274 Programming for GIS taught by Professor Shadrock Roberts at Clark University. Author: Arpita Shalini. 

In this tutorial we will learn how to create an interactive point and polyline map with folium in google Colab. Folium is a Python library used for visualizing geospatial data. It is easy to use and yet a powerful library. I have used Google Colab notebooks for writing my code. Colab notebooks allows us to combine executable code and rich text in a single document, along with images, HTML, LaTeX and more. I have focused on Worcester communityand have covered Clark University, University of Massachusetts Cancer Center and the Union Station. We also traverse along the routes of Clark University to Union station and Union Station to UMass routes. 


# Why folium?

folium builds on the data wrangling strengths of the Python ecosystem and the mapping strengths of the leaflet.js library. It manipulates your data in Python, then visualizes it in on a Leaflet map via folium.

folium makes it easy to visualize data that’s been manipulated in Python on an interactive leaflet map. It enables both the binding of data to a map for choropleth visualizations as well as passing rich vector/raster/HTML visualizations as markers on the map.

The library has a number of built-in tilesets from OpenStreetMap, Mapbox, and Stamen, and supports custom tilesets with Mapbox or Cloudmade API keys. folium supports both Image, Video, GeoJSON and TopoJSON overlays.

Our learning from this tutorial is:
* Learn to make maps using folium
* Add interactivity using folium
* Add polyline using folium. 

# Getting started

Although folium comes installed in Gooogle Colab, but we start by installing it again or run it. 

```
pip install folium

```
folium.map() takes location parameter and creates a map around it. We use coordinates of Worcester and map it. 

```
import folium     
 # Plotting maps using folium centering around Worcester
WOmap = folium.Map(location = [42.27199589252885, -71.80396347794411])        
WOmap 

```
We can zoom in an out as much as we want. But while scrolling it can become irritating and thus we would want to set a particular width and height of the map in pixels. 

```
# resizing the map by using Branca library in python. 
from branca.element import Figure                                               
fig = Figure(width = 600, height = 450)

```
<img src = Worcester1.jpg>

In the above code we use [branca](https://github.com/python-visualization/branca) library in python. We also want to set a zoom level for Worcester which we do through the following code:

```
#Setting minimum and maximum zoom levels
map1 = folium.Map(width=600, height=450, location=[42.27199589252885, -71.80396347794411], zoom_start=11, min_zoom=8, max_zoom=14)             
fig.add_child(map1)
map1 

```

# Interactivity using different basemaps

Folium creates map using different tileset such as Stamen Terrain, Stamen Toner, Stamen Water Color, CartoDB Positron.  Each tileset shows different features of a map and is suitable for different purposes. We will proceed by plotting a single map and giving an option to user to switch between them. 

```
# In this chunk we give an option to chose between different basemaps
fig2 = Figure(width = 600, height = 450) 

# Setting the zoom to Worcester. 
map2 = folium.Map(location = [42.27199589252885, -71.80396347794411])           
fig2.add_child(map2)

# Stamen Terrain as an option for basemap
folium.TileLayer('Stamen Terrain').add_to(map2) 

# Stamen Toner as an option for basemap
folium.TileLayer('Stamen Toner').add_to(map2)  

# Stamen Water Color as an option for basemap  
folium.TileLayer('Stamen Water Color').add_to(map2) 

# CartoDB Positron as an option for basemap
folium.TileLayer('cartodbpositron').add_to(map2)   

# CartoDB Dark Matter as an option for basemap
folium.TileLayer('cartodbdark_matter').add_to(map2)  

# Bar to chose between different layers. 
folium.LayerControl().add_to(map2)                                             
map2

```
# Plotting Interactive markers on the map

Markers are used for marking locations on a map. Markers are very helpful to identify locations and places on a map. folium uses folium.Marker() class for plotting markers on a map. we pass the coordinates, the pop-up message along with a hyperlink and the tooltip to display a marker. we include the hyperlinks so that the user can know more the marker by just clicking on it. We add four markers for Worcester Regional Airport, Union Station, Clark University and University of Massachusetts Cancer Center. 

```
fig3 = Figure(width = 600, height = 450)                                        # Creating Basemap
map3 = folium.Map(location=[42.268102601819336, -71.87604845525298], tiles = 'cartodbdark_matter', zoom_start = 11)   
fig3.add_child(map3)

# Adding markers to the map
# Adding a marker to represent Worcester Regional Airport, Click on the marker to explore more
folium.Marker(location=[42.268102601819336, -71.87604845525298],icon=folium.Icon(color="white"), popup="<a href=https://en.wikipedia.org/wiki/Worcester_Regional_Airport>Worcester Regional Airport</a>", tooltip='<strong>Worcester Regional Airport</strong>').add_to(map3)

# Adding a marker to represent Union Station. Click on the marker to explore more.
folium.Marker(location=[42.26036845049694, -71.79427754073927],icon=folium.Icon(color= "blue"), popup="<a href=https://en.wikipedia.org/wiki/Union_Station_(Worcester,_Massachusetts)>Worcester Union Station</a>",tooltip='<strong>Union Station</strong>').add_to(map3)

# Adding a marker to represent Clark University. Click on the marker to explore more. 
folium.Marker(location=[42.25182757196341, -71.82378344420422],icon=folium.Icon(color= "red"), popup="<a href=https://en.wikipedia.org/wiki/Clark_University>Clark University</a>",tooltip='<strong>Clark University</strong>').add_to(map3)

#Adding a marker to represent University of Massachusetts Cancer Center. Click on the pop-up to know more about it. 
folium.Marker(location=[42.27801397352389, -71.76045919601029],icon=folium.Icon(color= "purple"), popup="<a href=https://en.wikipedia.org/wiki/University_of_Massachusetts_Medical_School>UMass</a>",tooltip='<strong>University of Massachusetts</strong>').add_to(map3)
map3

```

# Plotting Polyline using Folium

We plot the path traveled by two cars from Clark University to Union Station and Union Station to UMass respectively. We note the coordinates of both the path traveled. We shall first create a basemap for the cars, create a feature group for each vehicle and the create paths and add them to feature groups and finally adding all the layers to the map. 

```
#Input the coordinates for the road traversed by car 1 from Clark University to Union Station

coords_1=[[42.25025514551179, -71.82217411887169],[42.25077135043246, -71.82120852357623],[42.25104930519409, -71.8206774462956],[42.25143049828775, -71.82006590265674],[42.2518990449694, -71.81916468040758],
[42.25220837127047, -71.81853424540093],[42.25231325367883, -71.81838630938444],[42.25249954347051, -71.81806710755652],[42.25279033618253, -71.81748395032945],
[42.25295390650431, -71.8171463330104],[42.253199261175894, -71.81667980722875],[42.25336737401422, -71.816403574869],[42.25352639925657, -71.81613348099542],
[42.25365816273286, -71.81588794112349],[42.253567291404735, -71.81607209603732],[42.25379446947952, -71.81574675568957],[42.25399438550848, -71.81541527684472],
[42.25416703975905, -71.8151083520163],[42.25462139078034, -71.81435945538671],[42.25512117312167, -71.81326066442621],[42.25538923655834, -71.81267136870203],
[42.255743623759656, -71.81200841101233],[42.2558980996088, -71.8117567326301],[42.25599351098392, -71.81156643925172],[42.25649328244147, -71.81052903323727],
[42.256743166703345, -71.81014844646727],[42.257083916348826, -71.80951004276608],[42.2578244725839, -71.80807977297846],[42.258546847259865, -71.8066986111249],
[42.25894210537229, -71.80611545389785],[42.259169264100734, -71.80579011356619],[42.2598416491181, -71.80491230850984],[42.26033230391483, -71.80432301278566],
[42.26065031889666, -71.80400994946845],[42.2612272847983, -71.80352500819544],[42.26171792881284, -71.80307075940804],[42.26215405363694, -71.80276383456872],
[42.26263106169122, -71.80249987919228],[42.26309443748834, -71.80235255526122],[42.26334883844795, -71.80219909285684],[42.26315803783146, -71.80166504360679],
[42.26315803783146, -71.80166504360679],[42.26305809442094, -71.80143178071596],[42.26284457842228, -71.80076882302625],[42.262626518783705, -71.80012428082794],
[42.26251294575096, -71.79989715650075],[42.262135881833856, -71.79874311904089],[42.26202230792296, -71.79834411672763],[42.26190873380748, -71.79788372944311],
[42.26185421816007, -71.79752769667738],[42.2618405892407, -71.7969629549417],[42.26178153055597, -71.79576594800196],[42.261776987577925, -71.79545288464848],
[42.26170884285786, -71.79526259126315],[42.2615498382484, -71.79499863588669],[42.26149532228998, -71.79478378848725]]

#Input the coordinates for the road traversed by car 2 from Union Station to Umass
coords_2=[[42.26146715715911, -71.79469133279913],[42.26145892503175, -71.79442437503852],[42.26152889807992, -71.79430201939822],
[42.261446576838715, -71.79415741727789],[42.26130251440804, -71.79404618487762],[42.26122842502975, -71.79402393839756],[42.26103202050461, -71.793902603609658],
[42.260853363733894, -71.79385432385152],[42.26065088544848, -71.793779222005532],[42.260452381426184, -71.7937643630732],[42.26030151435506, -71.7937268121471],
[42.260325335495544, -71.79348541333646],[42.26036503737637, -71.79335666730412],[42.26036900756308, -71.79293287828101],[42.26038885849285, -71.79266465738031],
[42.26037297774954, -71.7922462327752],[42.26036106718405, -71.7916025026065],[42.26036900755771, -71.79074419572424],[42.26034518643372, -71.79037405088128],
[42.26036900756, -71.78973032071366],[42.26035709699914, -71.78840530946418],[42.26036503737328, -71.78756309583599],[42.26061118848473, -71.7870910270448],
[42.261043935675055, -71.78654922082538],[42.26143697871451, -71.78606105878612],[42.261607693636066, -71.78578210904534],[42.26264785350638, -71.78452147081205],
[42.26328702722841, -71.78371144368597],[42.2643152496005, -71.78235424592472],[42.26445419728596, -71.7821718557104],[42.26512511178751, -71.78104532792513],
[42.26577616992544, -71.77980614736043],[42.266570134164304, -71.77822900845962],[42.266776563224084, -71.77766038015012],[42.266907565930644, -71.7766947849076],
[42.26694329390607, -71.77671087815585],[42.26712987294274, -71.7755521638648],[42.26730454218502, -71.77472067906761],[42.26749905963255, -71.77363706662634],
[42.26763006083768, -71.77314354016903],[42.26784839557465, -71.77291287019442],[42.26826521433626, -71.77246225908124],[42.26846369849212, -71.77227450445075],
[42.26895990617555, -71.77190435960257],[42.269781617462954, -71.77129281594895],[42.2702182712985, -71.77096558644601],[42.27100821007427, -71.77043987347865],
[42.27219905383205, -71.7696566684462],[42.27290561049429, -71.76871789529224],[42.27352086405807, -71.76807416512858],[42.273612159234744, -71.7679293258422],
[42.27367963819339, -71.76776839330178],[42.27377887182487, -71.76767719819554],[42.273945583974, -71.76754308774518],[42.27433060799022, -71.76717830731631],
[42.27547772740547, -71.76609469487482],[42.27618821649011, -71.7657460077039],[42.276065171467934, -71.76456583574083],[42.27597387984933, -71.76391674115314],
[42.275684127299336, -71.76175488069346],[42.27576748090913, -71.76163149907913],[42.27574366560331, -71.76140619352255],[42.27583495756818, -71.76114333703363],
[42.27601357188379, -71.76118088795974],[42.27644224417581, -71.76092876031306]]

```
```
fig5 = Figure(height = 600, width = 750)
map5 = folium.Map(location=[42.271487800314624, -71.80636673734611],tiles='Stamen Toner',zoom_start=12)
fig5.add_child(map5)

# Creating feature groups
C1=folium.FeatureGroup("Car 1")
C2=folium.FeatureGroup("Car 2")


# Adding lines to the different feature groups
line_1=folium.vector_layers.PolyLine(coords_1,popup='<b>Path of Ray</b>',tooltip='Car1',color='yellow',weight=10).add_to(C1)
line_2=folium.vector_layers.PolyLine(coords_2,popup='<b>Path of Sam</b>',tooltip='Car2',color='red',weight=10).add_to(C2)

C1.add_to(map5)
C2.add_to(map5)

folium.LayerControl().add_to(map5)
map5

```
