# Links
[Basic Editing Geoprocessing Tools in QGIS](https://grindgis.com/software/qgis/basic-editing-tools-in-qgis)

[How to remove the overlapping part of polygons?](https://gis.stackexchange.com/questions/201668/how-to-remove-the-overlapping-part-of-polygons)

[QGIS Change Attribute Type](https://wiki.tuflow.com/index.php?title=QGIS_Change_Attribute_Type)

[Merge Shapefile polygons using Quantum GIS](http://www.studytrails.com/blog/merge-shapefile-polygons-using-quantum-gis/)

# merge-shape-files
Merge shape files

```python
ogr2ogr -lco ENCODING=UTF-8 -f 'ESRI Shapefile' merge.shp ne_10m_admin_0_countries.shp
```

next merge another shape file with merge.shp

```python
ogr2ogr -f 'ESRI Shapefile' -update -append merge.shp ne_10m_admin_0_disputed_areas.shp -nln merge
```
Where
#### -f format_name:

output file format name, some possible values are:
<pre>
     -f "ESRI Shapefile"
     -f "TIGER"
     -f "MapInfo File"
     -f "GML"
     -f "PostgreSQL"
</pre> 

#### -append:

Append to existing layer instead of creating new

#### -overwrite:

Delete the output layer and recreate it empty

#### -update:

Open existing output datasource in update mode rather than trying to create a new one

#### -select field_list:

Comma-delimited list of fields from input layer to copy to the new layer. A field is skipped if mentioned previously in the list even if the input layer has duplicate field names. (Defaults to all; any field is skipped if a subsequent field with same name is found.) Starting with OGR 1.11, geometry fields can also be specified in the list.

#### -nln name:
Assign an alternate name to the new layer

[Refer the official document](http://www.gdal.org/ogr2ogr.html)


### Bash command


```bash
#!/bin/bash

file="./final/merge.shp"

for i in $(ls *.shp)
do

      if [ -f "$file" ]
      then
           echo "creating final/merge.shp" 
           ogr2ogr -f 'ESRI Shapefile' -update -append $file $i -nln merge
      else
           echo "merging……"
      ogr2ogr -f 'ESRI Shapefile' $file $i -lco ENCODING=UTF-8
fi
done
```
## Convert Shapefiles into GeoJSON

```bash
ogr2ogr -f "GeoJSON" w.geojson merge.shp
```
select only required fields

```bash
ogr2ogr -select NAME,ISO_A2 -f "GeoJSON" world_with_ant.geojson merge.shp
```
select and where 

```bash
ogr2ogr -select NAME,ISO_A2 -where 'ISO_A2!="AQ"' -f "GeoJSON" world_without_ant.geojson merge.shp
```

## Convert GeoJSON into topoJSON

```bash
geo2topo input.geojson > output.topojson
```
