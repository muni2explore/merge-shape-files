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
-f format_name:

output file format name, some possible values are:
<pre>
     -f "ESRI Shapefile"
     -f "TIGER"
     -f "MapInfo File"
     -f "GML"
     -f "PostgreSQL"
</pre> 

-append:

Append to existing layer instead of creating new

-overwrite:

Delete the output layer and recreate it empty

-update:

Open existing output datasource in update mode rather than trying to create a new one

-select field_list:

Comma-delimited list of fields from input layer to copy to the new layer. A field is skipped if mentioned previously in the list even if the input layer has duplicate field names. (Defaults to all; any field is skipped if a subsequent field with same name is found.) Starting with OGR 1.11, geometry fields can also be specified in the list.

Bash command


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
      ogr2ogr -f 'ESRI Shapefile' $file $i
fi
done
```
