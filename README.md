# QGis-Plugins
Repository for saving plugins for managing geographic information, developed in QGis

## 1. Test
This test plugin was created to perform the reprojection of shapefile-type vector layers contained in a folder, its use is simple:

![Image Plugin UI](https://github.com/fernandezjavier480/GithubTest/blob/a6213e83f7c56a300ab755703ca6241a63162e50/1_Image.PNG)

1. Select input folder containing all shapefiles whose projection will be transformed
2. Select output folder, a "Results" subfolder will be created in it with the reprojected elements
3. Select the projection to which you want to transform your data

The transformed data is added to the current project and verification of your new projection can be done by opening the properties of each layer.

![Image of the result added to the project](https://github.com/fernandezjavier480/GithubTest/blob/3d25468701585c0e8d85b94d78367c1767dea496/2_Image.png)

The code that allows this reprojection is found in the Test.py file, which is made up of the following lines:

```python
def projection(self):
        """Reproject all shapefiles in folder"""
        # Create Path Results
        respath = 'Results'
        # Mode create output
        mode = 0o666
        # Create pathout
        pathout = os.path.join(self.folder_path_out, respath)
        os.mkdir(pathout, mode)
        # Iterate directory
        for file in os.listdir(self.folder_path_in):
        # check only shapefiles
            if file.endswith('.shp'):
                #Run processing with parameters
                processing.runAndLoadResults("qgis:reprojectlayer", 
                               {'INPUT': self.folder_path_in + '\\' + file,
                                'TARGET_CRS': self.project,
                                'OUTPUT' : pathout + '\\proj_' + file})

    
    def run(self):
        """Run method that performs all the real work"""

        # Create the dialog with elements (after translation) and keep reference
        # Only create GUI ONCE in callback, so that it will only load when the plugin is started
        if self.first_start == True:
            self.first_start = False
            self.dlg = TestDialog()
            #Change mode of storage to Folder in two widgets
            self.Widfolder_in = self.dlg.mQgsFileWidget.setStorageMode(1)
            self.Widfolder_out = self.dlg.mQgsFileWidget_2.setStorageMode(1)
            
        # show the dialog
        self.dlg.show()
        # Run the dialog event loop
        result = self.dlg.exec_()
        # See if OK was pressed
        if result:
            # Do something useful here - delete the line containing pass and
            # substitute with your code.
            # Folder selected 
            self.folder_path_in = self.dlg.mQgsFileWidget.filePath()
            self.folder_path_out = self.dlg.mQgsFileWidget_2.filePath()
            # CRC selected
            self.project = self.dlg.mQgsProjectionSelectionWidget.crs().authid()
            # Execute projection function 
            self.projection()
```
#### The plugin is a test so its use is basic and simple for those who are just getting into spatial data management in QGIS
