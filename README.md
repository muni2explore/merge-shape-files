# merge-shape-files
Merge shape files

```python
ogr2ogr -lco ENCODING=UTF-8 -f 'ESRI Shapefile' merge.shp ne_10m_admin_0_countries.shp
```

next merge another shape file with merge.shp

```python
ogr2ogr -f 'ESRI Shapefile' -update -append merge.shp ne_10m_admin_0_disputed_areas.shp -nln merge
```

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
