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
