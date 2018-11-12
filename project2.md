# Project 2
Maria Rochford

## Goal:
My goal for this project is to look at the state of Maryland in three different time periods and compare the median household income of each county. I used the years 2016, 2000, and 1990. I also brought in data for tornadoes in the state from these time periods. The dataset of these storms include monetary damage as well as fatalities and injuries. I want to look and see if a greater amount of damage correlates with a lower income rate in the 2000 map and the 1990 map. I will then look at the 2016 map to predict the amount of damage the same type of storm would cause if it happened today.

## Step 1
Adding the data.
```python
layer = iface.addVectorLayer('Z:/lab_2/Maryland_Physical_Boundaries__County_Boundaries_Detailed(1)/Maryland_Physical_Boundaries__County_Boundaries_Detailed.shp', 'Median Household Income', 'ogr')
```
## Step 2
I need to classify the data so that it shows each county by it's median household income for the 2000s.
```python
from qgis.PyQt import QtGui

myVectorPath = ('Z:/lab_2/Maryland_Physical_Boundaries__County_Boundaries_Detailed(1)/Maryland_Physical_Boundaries__County_Boundaries_Detailed.shp')
myName = ('MedianHouseholdIncome2000')
myVectorLayer = QgsVectorLayer(myVectorPath, myName, 'ogr')
myTargetField = 'MHInc2000'
myRangeList = []
myOpacity = 1
# First Range
myMin = 0.0
myMax = 35000.0
myLabel = 'Lowest'
myColour = QtGui.QColor('#fff5f0')
mySymbol1 = QgsSymbol.defaultSymbol(myVectorLayer.geometryType())
mySymbol1.setColor(myColour)
mySymbol1.setOpacity(myOpacity)
myRange1 = QgsRendererRange(myMin, myMax, mySymbol1, myLabel)
myRangeList.append(myRange1)
# Second Range
myMin2 = 35001.0
myMax2 = 41000.0
myLabel2 = 'Low'
myColour2 = QtGui.QColor('#fdcab5')
mySymbol2 = QgsSymbol.defaultSymbol(myVectorLayer.geometryType())
mySymbol2.setColor(myColour2)
mySymbol2.setOpacity(myOpacity)
myRange2 = QgsRendererRange(myMin2, myMax2, mySymbol2, myLabel2)
myRangeList.append(myRange2)
# Third Range
myMin3 = 41001.0
myMax3 = 56000.0
myLabel3 = 'Medium'
myColour3 = QtGui.QColor('#fc8a6a')
mySymbol3 = QgsSymbol.defaultSymbol(myVectorLayer.geometryType())
mySymbol3.setColor(myColour3)
mySymbol3.setOpacity(myOpacity)
myRange3 = QgsRendererRange(myMin3, myMax3, mySymbol3, myLabel3)
myRangeList.append(myRange3)
# Fourth Range
myMin4 = 56001.0
myMax4 = 62000.0
myLabel4 = 'High'
myColour4 = QtGui.QColor('#f96245')
mySymbol4 = QgsSymbol.defaultSymbol(myVectorLayer.geometryType())
mySymbol4.setColor(myColour4)
mySymbol4.setOpacity(myOpacity)
myRange4 = QgsRendererRange(myMin4, myMax4, mySymbol4, myLabel4)
myRangeList.append(myRange4)
# Fifth Range
myMin5 = 62001.0
myMax5 = 75000.0
myLabel5 = 'Highest'
myColour5 = QtGui.QColor('#d42020')
mySymbol5 = QgsSymbol.defaultSymbol(myVectorLayer.geometryType())
mySymbol5.setColor(myColour5)
mySymbol5.setOpacity(myOpacity)
myRange5 = QgsRendererRange(myMin5, myMax5, mySymbol5, myLabel5)
myRangeList.append(myRange5)

myRenderer = QgsGraduatedSymbolRenderer('', myRangeList)
myRenderer.setMode(QgsGraduatedSymbolRenderer.EqualInterval)
myRenderer.setClassAttribute(myTargetField)

myVectorLayer.setRenderer(myRenderer)
QgsProject.instance().addMapLayer(myVectorLayer)
```
## Step 3
Add the tornadoes onto the 2000s map and fix the symbology
```python
TornadoesF2 = iface.addVectorLayer('Z:/Project_2/Data/2000F2.shp', '2000s F2 Tornadoes', 'ogr')
renderer = TornadoesF2.renderer()
renderer
symbol = renderer.symbol()
symbol.setColor(QColor('#4daf4a'))
TornadoesF2.triggerRepaint()

TornadoesF3 = iface.addVectorLayer('Z:/Project_2/Data/2000F3.shp', '2000s F3 Tornadoes', 'ogr')
renderer = TornadoesF3.renderer()
renderer
symbol = renderer.symbol()
symbol.setColor(QColor('#1e77b2'))
TornadoesF3.triggerRepaint()

TornadoesF4 = iface.addVectorLayer('Z:/Project_2/Data/2000F4.shp', '2000s F4 Tornadoes', 'ogr')
renderer = TornadoesF4.renderer()
renderer
symbol = renderer.symbol()
symbol.setColor(QColor('#010401'))
TornadoesF4.triggerRepaint()
```
## Step 4
Classify the data for the 1990's Map
```python
from qgis.PyQt import QtGui

myVectorPath = ('Z:/lab_2/Maryland_Physical_Boundaries__County_Boundaries_Detailed(1)/Maryland_Physical_Boundaries__County_Boundaries_Detailed.shp')
myName = ('MedianHouseholdIncome1990')
myVectorLayer = QgsVectorLayer(myVectorPath, myName, 'ogr')
myTargetField = 'MHInc1980' #Don't panic, I just accidentally called the field the wrong year. It's still 1990 NOT 1980
myRangeList = []
myOpacity = 1
# First Range
myMin = 0.0
myMax = 31000.0
myLabel = 'Lowest'
myColour = QtGui.QColor('#fff5f0')
mySymbol1 = QgsSymbol.defaultSymbol(myVectorLayer.geometryType())
mySymbol1.setColor(myColour)
mySymbol1.setOpacity(myOpacity)
myRange1 = QgsRendererRange(myMin, myMax, mySymbol1, myLabel)
myRangeList.append(myRange1)
# Second Range
myMin2 = 31001.0
myMax2 = 40000.0
myLabel2 = 'Low'
myColour2 = QtGui.QColor('#fdcab5')
mySymbol2 = QgsSymbol.defaultSymbol(myVectorLayer.geometryType())
mySymbol2.setColor(myColour2)
mySymbol2.setOpacity(myOpacity)
myRange2 = QgsRendererRange(myMin2, myMax2, mySymbol2, myLabel2)
myRangeList.append(myRange2)
# Third Range
myMin3 = 40001.0
myMax3 = 47200.0
myLabel3 = 'Medium'
myColour3 = QtGui.QColor('#fc8a6a')
mySymbol3 = QgsSymbol.defaultSymbol(myVectorLayer.geometryType())
mySymbol3.setColor(myColour3)
mySymbol3.setOpacity(myOpacity)
myRange3 = QgsRendererRange(myMin3, myMax3, mySymbol3, myLabel3)
myRangeList.append(myRange3)
# Fourth Range
myMin4 = 47201.0
myMax4 = 51000.0
myLabel4 = 'High'
myColour4 = QtGui.QColor('#f96245')
mySymbol4 = QgsSymbol.defaultSymbol(myVectorLayer.geometryType())
mySymbol4.setColor(myColour4)
mySymbol4.setOpacity(myOpacity)
myRange4 = QgsRendererRange(myMin4, myMax4, mySymbol4, myLabel4)
myRangeList.append(myRange4)
# Fifth Range
myMin5 = 51001.0
myMax5 = 75000.0
myLabel5 = 'Highest'
myColour5 = QtGui.QColor('#d42020')
mySymbol5 = QgsSymbol.defaultSymbol(myVectorLayer.geometryType())
mySymbol5.setColor(myColour5)
mySymbol5.setOpacity(myOpacity)
myRange5 = QgsRendererRange(myMin5, myMax5, mySymbol5, myLabel5)
myRangeList.append(myRange5)

myRenderer = QgsGraduatedSymbolRenderer('', myRangeList)
myRenderer.setMode(QgsGraduatedSymbolRenderer.EqualInterval)
myRenderer.setClassAttribute(myTargetField)

myVectorLayer.setRenderer(myRenderer)
QgsProject.instance().addMapLayer(myVectorLayer)
```
## Step 5
Add the tornadoes onto the 1990's map and fix the symbology
```python
TornadoesF20 = iface.addVectorLayer('Z:/Project_2/Data/1990F2.shp', '1990s F2 Tornadoes', 'ogr')
renderer = TornadoesF20.renderer()
renderer
symbol = renderer.symbol()
symbol.setColor(QColor('#4daf4a'))
TornadoesF20.triggerRepaint()

TornadoesF30 = iface.addVectorLayer('Z:/Project_2/Data/1990F3.shp', '1990s F3 Tornadoes', 'ogr')
renderer = TornadoesF30.renderer()
renderer
symbol = renderer.symbol()
symbol.setColor(QColor('#1e77b2'))
TornadoesF30.triggerRepaint()
```
## Results:

The results that I found from these two maps were not very useful. I had thought that the most amount of tornado damage would occur in counties that had the lowest median household income because of poorer infrastructure. The results did not show that and instead seem to be random and not correlated. The darker the red, the higher the median household income!

**2000s**
![2000sMap](2000sMap.png)
![2000sChart](2000sChart.png)

**1990s**
![1990sMap](1990sMap.png)
![1990sChart](1990sChart.png)
