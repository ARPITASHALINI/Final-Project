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
In the above code we use [branca](https://github.com/python-visualization/branca) library in python. 
