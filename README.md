# 🌍 ArcGIS Pro & Python (ArcPy) Cheat Sheet

Este repositorio es un resumen de las herramientas más utilizadas en **ArcGIS Pro** y su implementación mediante automatización con el paquete **ArcPy** de Python. 

> *Nota personal: Este recurso fue creado para centralizar flujos de trabajo y facilitar la transición de la interfaz visual al scripting.*


---
<br>

## 🛠 Analysis toolbox

Las herramientas del conjunto de herramientas Extraer permiten seleccionar entidades y atributos en una clase de entidad o una tabla basándose en una consulta (expresión SQL) o una extracción espacial y de atributo. Las entidades y atributos de salida se almacenan en una clase de entidad o una tabla.

### 1. Clip  |  Recortar
Extrae entidades de entrada que se superponen a las entidades del clip.
- **Herramienta:** `Analysis Tools -> Extract -> Clip`
- **Python:** `arcpy.analysis.Clip(in_features, clip_features, out_feature_class, {cluster_tolerance})`

```python
# Recorta las líneas de Ferrocarril que pasan por la Comunidad de Cantábria.

import arcpy

# Definir rutas
in_features = "ferrocarril.shp"
clip_features = "comunidad_Cantabria.shp"
out_feature_class = "C:/output/miEstudioCantabria.shp"

# Ejecución
arcpy.analysis.Clip(in_features, clip_features, out_feature_class)
```


### 2. Select  |  Seleccionar
Extrae entidades de una clase de entidad de entrada o una capa de entidades de entrada, generalmente mediante una expresión de selección o SQL y las almacena en una clase de entidad de salida.
- **Herramienta:** `Analysis Tools -> Extract -> Select`
- **Python:** `arcpy.analysis.Select(in_features, out_feature_class, {where_clause})`

```python
# Extrae de la capa de Comunidades Autónomas la entidad/es cuyo valor en el campo nombre sea Cantabria.

import arcpy

# Definir rutas
in_features = "comunidades.shp"
out_feature_class = "C:/output/cantabria.shp"
where_clause = '"NOMBRE" = \'Cantabria\''

# Ejecución
arcpy.analysis.Clip(in_features, clip_features, out_feature_class)
```

### 3. Split  |  Dividir  
Divide una entrada con entidades de superposición para crear un subconjunto de clases de entidad de salida.
- **Herramienta:** `Analysis Tools -> Extract -> Split`
- **Python:** `arcpy.analysis.Split(in_features, split_features, split_field, out_workspace, {cluster_tolerance})`

```python
import arcpy

# Definir rutas
in_feature = "DatosComunidades.gdb/CCAA"
splitFeatures = "comunidades.shp"
splitField = "Nombre"
outWorkspace = "C:/output/Output.gdb"
clusterTol = "1 Meters"

# Ejecución
arcpy.analysis.Split(in_feature, splitFeatures, splitField, outWorkspace, clusterTol)
```


### 4. Split By Attributes  |  Dividir por atributos 
Divide un dataset de entrada por atributos únicos.
- **Herramienta:** `Analysis Tools -> Extract -> Split By Attributes`
- **Python:** `arcpy.analysis.SplitByAttributes(Input_Table, Target_Workspace, Split_Fields)`

```python
import arcpy

# Definir rutas
in_feature_class = 'c:/data/base.gdb/ecology'
target_workspace = 'c:/data/output.gdb'
fields = ['REGION', 'ECO_CODE']

# Ejecución
arcpy.analysis.SplitByAttributes(in_feature_class, target_workspace, fields)
```


### 5. Table Select  |  Seleccionar tabla 
Selecciona los registros de tabla que coinciden con una expresión de Lenguaje estructurado de consultas (SQL) y los escribe en una tabla de salida.
- **Herramienta:** `Analysis Tools -> Extract -> Table Select`
- **Python:** `arcpy.analysis.TableSelect(in_table, out_table, {where_clause})`

```python
import arcpy

# Definir rutas
in_features = "majorrds.shp"
out_feature_class = "C:/output/majorrdsCl4.shp"
where_clause = '"CLASS" = \'4\''

# Ejecución
arcpy.analysis.TableSelect(in_features, out_feature_class, where_clause)
```

### 6. Intersect  |  Intersecar 
Calcula una intersección geométrica de las entidades de entrada. Las entidades o partes de entidades que se superponen con todas las capas o clases de entidad se escriben en la clase de entidad de salida.
- **Herramienta:** `Analysis Tools -> Overlay -> Intersect`
- **Python:** `arcpy.analysis.Intersect(in_features, out_feature_class, {join_attributes}, {cluster_tolerance}, {output_type})`

```python
import arcpy

# Definir rutas
in_features =["vegetation_stands", "road_buffer200m", "water_buffer100"]
out_feature_class = "mysites"

# Ejecución
arcpy.analysis.Intersect(in_features,out_feature , "ALL")
```









---
<br>

## 📚 Fuentes y Referencias
Toda la información técnica, sintaxis de código y conceptos de herramientas presentados en este resumen han sido adaptados de la documentación oficial de **Esri**.

* [Documentación de ArcPy (ArcGIS Pro)](https://pro.arcgis.com/es/pro-app/latest/arcpy/main/arcgis-pro-arcpy-reference.htm)
* [Herramientas de Geoprocesamiento de ArcGIS Pro](https://pro.arcgis.com/es/pro-app/latest/tool-reference/main/arcgis-pro-tool-reference.htm)
* [Guía de aprendizaje de Python en ArcGIS](https://learn.arcgis.com/)

---
*Este repositorio tiene fines educativos y de consulta rápida.*



