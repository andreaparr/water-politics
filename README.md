## Western Watersheds & Biodiversity

### I. Introduction

This map will explore possible relationships between water reclamation projects and biodiversity in western watersheds. There is an overwhelming amount of data and a lot of confusing measurements that federal agencies use to track the health of the environment (see [resources](#resources) below for some examples). My goal is to create a compelling story map that helps users understand a geographic feature (watersheds) that regulatory agencies like the EPA use to organize information. Specifically, I plan to look at at-risk species by watershed (the EPA measures this) and then (if appropriate!) examine the relationship between the status of species and water reclamation projects (which are tracked by the Bureau of Reclamation).

I do not have much (any) background knowledge in ecology or hydrology, so I am approaching this project as an investigative journalist. I expect that the map user is equally uninformed, so the story map should in many ways echo my research and development process. I am starting with a prototype map organized by watershed and categorized by the number of at-risk species. In the next section, a layer of points of Bureau of Water Reclaimation projects (reservoirs, dams, etc.). will appear. Finally, the story map will narrow down to one or more watersheds/sub-watersheds and include information that is specific to that region (i.e. Willow Flycatchers disapearing at Lake Havasu).

### II. Methodology

My plan is to map western water resource regions at the local sub-watershed level (hydrologic unit code 12, HUC12). Hydrologic unit code 12 (HUC12) captures tributary systems, of which there are about 90,000 nationwide. At this point, the smaller geographic area seems more precise, but I am not sure this is true/appropriate (MAUP, etc). I am open to finding out I'm wrong - watersheds are complex and this is something for which I will seek guidance.

Following are the HUCs:
* 2-digit HUC (region)
* 4-digit HUC (sub-region)
* 6-digit HUC (accounting unit)
* 8-digit HUC (cataloguing unit)
* 10-digit HUC (watershed)
* 12-digit HUC (sub-watershed)

#### A. Data

I am currently looking at capturing information from 4 of the 21 water resource regions. Specifically...

[USGS](https://water.usgs.gov/wsc/index.html):
* Great Basin (HUC16 - EPA8/9)
* Lower Colorado (HUC15 - EPA9/8)
* Pacific Northwest (HUC17 - EPA10)
* California (HUC18 - EPA9)

EPA Data:
* Watershed Index Online [(WSIO) Indicator Library](https://www.epa.gov/wsio/wsio-indicator-data-library) (Regions 8-10)

USBR - Reclamation Wter Information Systems (RWIS):
* This interactive [map](https://water.usbr.gov/RWISmap.php) has downloadable info about projects by HUC.

For the exploratory stage, I have simplified and downloaded sample files from the three primary sources (USGS, EPA, USBR).

USGS Data:
I combined and simplified four shapefiles using mapshaper in node. Note that this is for HUC-12. I am working on doing the same for HUC-2, HUC-4, and HUC-10.
 * [watersheds.json](data/watersheds-huc12.geojson)

 USBR data:
 To create this file, I combined four CSV files (downloaded by water resource region) and used a CSV to JSON tool.
 * [usbrpoints.json](data/usbrpoints.geojson)

 EPA data:
 I took table data from two of the three needed EPA region (9 and 10 of 8-10) xls files, clipped it down to just "at risk" species data, and joined the files. This will absolutely need to be expanded to include other columns in the future.
 * [epa_wsio_atrisk.csv](data/epa_wsio_atrisk.csv)

Here's a prototype of the EPA and USGS data joined using CartoDB:<iframe width="100%" height="520" frameborder="0" src="https://nmp.carto.com/u/andrearparr/builder/bc8fb5c2-6647-42d8-8c1d-4921a4ca09e5/embed" allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>


#### B. Medium for delivery

This map will be a story map that will use a variety of technologies including HTML/SVG/CSS/JS and Leaflet. I am primarily using the [storymap.js library by Bo Zhao](https://github.com/jakobzhao/storymap).

#### C. Application layout

Story map flow:
See [wireframe sketch](wireframes/wireframe-watersheds) for the overall flow. 
* Opens on map of HUC2 watersheds. Copy in transparent box to the left provides an introduction to watersheds.
* Panel 2 shows HUC4 areas and goes into more detail about watershed administration. There is a slight zoom.
* Panel 3 shows HUC10 areas - this is the actual watershed level
* Panel 4 zooms back out a bit and adds EPA data. This is sympbolized as a choropleth map.
* Panel 5 adds point level data for water reclamation project locations
* Panel 6 zooms into a local region (currently Lake Havasu, but subject to change in the next two weeks)

The flow on mobile devices will be the same, but some features may be modified.

#### D. Thematic representation

Aggregate data from the WISO will be represented in a choropleth map organized by sub-watersheds. Locations of reclamation projects will be represented as points. There may be a reason to include a statistical map if it becomes important to highlight other EPA/USBR data points. This is something that I will discover when interviewing experts in watersheds.

#### E. User interaction

In an ideal world, much of the map progression is going to be driven by scrolling - this is a trigger for many things to populate - copy blocks, maps, map layers. Additionally, I plan to encourage users to click on the watersheds/WISO layer to learn more about the sub-watersheds. 

#### F. Aesthetics and design considerations

I would like for the map to be clean and modern. The data here is complicated and unfamiliar, so the design should try to streamline information (hahaha, given all of this transparent layer, scrolling, etc. things I've written above). I am interested in bringing in design elements (palettes, typefaces, etc) that are represent featured locations.

### III. Conclusion

By the end of exploring this map, my goal is for the users to have a better understanding of what a watershed is and why it's a useful administrative unit. Additionally, I hope to highlight the breadth of water reclamtion projects that exisit and highlight their impact on sub-watersheds and the species that live in those areas. I do not expect to draw definitive conclusions, this project is about learning more about the connection between water management and biodiversity.

Ideally this type of map could help users develop a vocabulary to better understand environmental data and perhaps advocate for their interests.

#### <a name="resources"></a> Additional Resources

* There's a whole [Bureau of Reclaimation](https://www.usbr.gov) that has project information, news releases, and the [Reclamation Water Information System](https://water.usbr.gov/) which has "machine readable water datasets to use as input for models and analyses via automated data exchange via webservice.
* USBR made a neat storymap on [Irrigation Demand Projections](https://usbr.maps.arcgis.com/apps/MapJournal/index.html?appid=f08c6c521fe64e259b3da9771b948204).
* The EPA has an [EnviroAtlas](https://www.epa.gov/enviroatlas/enviroatlas-data-download-step-2) with data downloads. Their [interactive map](https://enviroatlas.epa.gov/enviroatlas/interactivemap/) has data on species at risk. 
* The EPA also has a [Surf Your Watershed](https://www.epa.gov/waterdata/surf-your-watershed) page that has, among other things, breakdowns of the 10 EPA regions (I am interested in 8-10) and (THERE IS SO MUCH DATA) and [national GIS datasets](https://www.epa.gov/wsio/wsio-indicator-data-library#huc).
* Endangered species info is available at [FWS](https://www.fws.gov/endangered/species/index.html).
* [Western Waters Digital Library](http://westernwaters.org) has primary and secondary resources on water in the western US. Archival materials. This would be a good source for old maps to georeference (among many other things).
* [Western Watersheds Project](https://www.westernwatersheds.org/about/) has news releases, action alerts, some general info about [species protection](https://www.westernwatersheds.org/issues/species/).
* Some potentially useful data from [Fish & Wildlife](https://ecos.fws.gov/ServCat/). Maybe [FWS Ecrosystem Regions](https://ecos.fws.gov/ServCat/Reference/Profile/74343)? will have interesting/useful layers?
* USGS has a [Watershed Boundary Dataset](https://www.usgs.gov/core-science-systems/ngp/national-hydrography/watershed-boundary-dataset?qt-science_support_page_related_con=4#qt-science_support_page_related_con) that may be useful as a layer.
* USGS's [ScienceBase-Catalog](https://www.sciencebase.gov/catalog/) may have other potential layers.
* USGS has [water budget](https://cida.usgs.gov/nwc-static/waterbudget-viz/) info - water budgets are "used to understand the movement of water into and out of a watershed". There might be something interesting here?
* The [Center for Biological Diversity](https://www.biologicaldiversity.org) has some basic information about endangered amphibians, birds, fish, invertebrates, mammals, plants, and reptiles.

#### Story maps for inspiration
Following are some storymaps that I've enjoyed.
* [Borderline](https://www.washingtonpost.com/graphics/2018/national/us-mexico-border-flyover/?utm_term=.27ecb945b600), Washington Post
* [Murder with impunity](https://www.washingtonpost.com/graphics/2018/politics/midterm-election-precinct-results/?utm_term=.cba9b1786834), Washington Post.


