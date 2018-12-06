# Lab 5
Maria Rochford

### 8.1
Code:
```python
from PyQt5.QtGui import QColor
from PyQt5.QtCore import Qt
from qgis.utils import iface

def load_layer():
	iface.addVectorLayer('Z:/lab_4/shapefiles/Files_used/pyqgis3_files/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')

def change_color():
	active_layer = iface.activeLayer()
	renderer = active_layer.renderer()
	symbol = renderer.symbol()
	symbol.setColor(QColor(Qt.red))
	active_layer.triggerRepaint()
	iface.layerTreeView().refreshLayerSymbology(active_layer.id())

def open_attribute_table():
	iface.showAttributeTable(iface.activeLayer())

exec(open('Z:/lab_5/pygis_scripts/script8.1.py'.encode('utf-8')).read())
```

Results:
![8.1.png](8.1.png)

### 8.2
Code:
```python
from PyQt5.QtGui import QColor
from PyQt5.QtCore import Qt
from qgis.utils import iface

active_layer = iface.activeLayer()
renderer = active_layer.renderer()
symbol = renderer.symbol()
symbol.setColor(QColor(Qt.red))
active_layer.triggerRepaint()
iface.layerTreeView().refreshLayerSymbology(active_layer.id())

iface.showAttributeTable(iface.activeLayer())

exec(open('Z:/lab_5/pygis_scripts/script8.2.py'.encode('utf-8')).read())
```
Results:
![8.2.png](8.2.png)

### 8.3
Code:
```python
from PyQt5.QtGui import QColor
from PyQt5.QtCore import Qt

class FirstScript:
	def __init__(self, iface):
		self.iface = iface
	def load_layer(self):
		self.iface.addVectorLayer('Z:/lab_4/shapefiles/Files_used/pyqgis3_files/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')
	def change_color(self):
		active_layer = self.iface.activeLayer()
		renderer = active_layer.renderer()
		symbol = renderer.symbol()
		symbol.setColor(QColor(Qt.red))
		active_layer.triggerRepaint()
		self.iface.layerTreeView().refreshLayerSymbology(active_layer.id())
	def open_attribute_table(self):
		self.iface.showAttributeTable(self.iface.activeLayer())

fs = FirstScript(qgis.utils.iface)
fs.iface
from first_script_class import FirstScript
fs = FirstScript(iface)
fs.load_layer()
fs.change_color()
fs.open_attribute_table()
```

### 8.4
Code:
```python
from PyQt5.QtGui import QColor
from PyQt5.QtCore import Qt

class FirstScript:
	def __init__(self, iface):
		self.iface = iface
	def load_layer(self):
		self.iface.addVectorLayer('Z:/lab_4/shapefiles/Files_used/pyqgis3_files/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')
	def change_color(self):
		active_layer = self.iface.activeLayer()
		renderer = active_layer.renderer()
		symbol = renderer.symbol()
		symbol.setColor(QColor(Qt.red))
		active_layer.triggerRepaint()
		self.iface.layerTreeView().refreshLayerSymbology(active_layer.id())
	def open_attribute_table(self):
		self.iface.showAttributeTable(self.iface.activeLayer())

def run_script(iface):
	fs = FirstScript(iface)
	fs.load_layer()
	fs.change_color()
	fs.open_attribute_table()

	exec(open('Z:/lab_5/pygis_scripts/script8.4.py'.encode('utf-8')).read())
```

### Chapter 9 Questions
*1. Find the qgis.utils module in your QGIS install and open it in a text editor. Examine the methods and data structures available.*
```python
import qgis.utils
pp = qgis.utils.plugins
```
*2. Create a point memory layer with an id and name field, add some features to it, and add it to the map canvas.*
```python
mem_layer = QgsVectorLayer(
"LineString?crs=epsg:4326&field=id:integer"
"&field=road_name:string&index=yes",
"Roads",
"memory")
QgsProject.instance().addMapLayer(mem_layer)

mem_layer.startEditing()
points = [QgsPoint(-150, 61), QgsPoint(-151, 62)]
feature = QgsFeature() feature.setGeometry(QgsGeometry.fromPolyline(points))
feature.setAttributes([1, 'QGIS Lane'])
mem_layer.addFeature(feature)
mem_layer.commitChanges()
```
![figure91.jpg](figure91.jpg)

![figure92.jpg](figure92.jpg)

![figure93.jpg](figure93.jpg)

*3. Write a script to turn on labeling for the point layer you created and label each feature using the name field.*
```python
import qgis.utils

if 'pinpoint' in qgis.utils.plugins:
    pp = qgis.utils.plugins['pinpoint']
pp

if 'pinpoint' in qgis.utils.plugins:
    pp = qgis.utils.plugins['pinpoint']
    pp.create_pin_layer()
    pp.place_pin(QgsPointXY(100,100), 1)
		```
*4. Using the point layer, write a script that allows you to edit the name for a selected feature by*
```python
wb = QgsVectorLayer('Z:/lab_4/shapefiles/Files_used/pyqgis3_files/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')

gml_lyr = QgsVectorLayer('Z:/lab_4/shapefiles/Files_used/pyqgis3_files/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')
QgsProject.instance().addMapLayer(gml_lyr)
idx = feature.fieldNameIndex('CNTRY_NAME')

layer = iface.activeLayer()
provider = layer.dataProvider()
feature = layer.getFeature(1)
feature['name'] = 'My New Name'
feature['city'] = 'Seattle'
field_map = provider.fieldNameMap()
attrs = {field_map[key]: feature[key] for key in field_map}
attrs
{0: 'Seattle', 1: 'My New Name'}
layer.dataProvider().changeAttributeValues({feature.id(): attrs})
```
