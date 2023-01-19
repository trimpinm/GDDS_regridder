# File type comparison
Author: Maggie Trimpin
ver 1.
Updated 1-26-2022

---

### In terms of grass: 

GRASS uses xarray (xarray.open-dataset only supports netCDF and HDF5)
* xarray.open_rasterio: Open a file with rasterio. ... This should work with any file that rasterio can open (most often: geoTIFF).
* xarray.open_zarr: load and decode a dataset from a Zarr store. The store object should be a valid store for a Zarr group. 

---

### General Info

| File Type        |   Description  | Strengths/ Advantages| Weaknesses/ Limiations
| :------- | :----------: | :------: | :-----: |
| **netCDF4**    |  NetCDF is a set of software libraries and self-describing, machine-independent data formats for array-oriented scientific data. The purpose of netCDF is to provide a data model, software libraries, and machine-independent data format for geoscience data. Together, the netCDF interfaces, libraries, and format support the creation, access, and sharing of scientific data. | <ul> <li>Self-Describing. A netCDF file includes information about the data it contains.</li><li>Portable. A netCDF file can be accessed by computers with different ways of storing integers, characters, and floating-point numbers.</li><li>Scalable. Small subsets of large datasets in various formats may be accessed efficiently through netCDF interfaces, even from remote servers.</li><li>Appendable. Data may be appended to a properly structured netCDF file without copying the dataset or redefining its structure.</li><li>Sharable. One writer and multiple readers may simultaneously access the same netCDF file.</li><li>Archivable. Access to all earlier forms of netCDF data will be supported by current and future versions of the software.</li> </ul>  | <ul><li>No real data structures, just multidimensional arrays and lists<li>No nested structures, variable-length types, or ragged arrays<li>Only one shared unlimited dimension for appending new data<li>A flat name space for dimensions and variables<li>Character arrays rather than "real" strings<li> small set of numeric types </ul>|
|**HDF5** | The Hierarchical Data Format version 5 (HDF5), is an open source file format that supports large, complex, heterogeneous data. HDF5 uses a "file directory" like structure that allows you to organize data within the file in many different structured ways, as you might do with files on your computer. | <ul><li>Hierarchical structure (similar to folders/files)<li>optional arbitrary metadata stored with each item <li>flexibility (e.g. compression)<li>datasets can be either fixed-size or flexibly sized (easy to append data to a large dataset without having to create an entire new copy)</Ul> | <ul><li>HDF5 is undeniably complex, and requires a significant learning curve<li>A major limitation for HDF5 is the loss of backward compatibility with HDF4 and earlier versions. Also, unlike less complex formats, users cannot read the HDF5 files directly without using the HDF5 software library.<li>use of netCDF and HDF5 in high performance computing applications with thousands of processors using parallel I/O, which warn of the danger of file corruption during parallel I/O if a client dies at a particular time </ul>
|**geoTIFF**|  GeoTIFF is a public domain metadata standard that enables georeferencing information to be embedded within an image file. The GeoTIFF format embeds geospatial metadata into image files such as aerial photography, satellite imagery, and digitized maps so that they can be used in GIS applications. The purpose of Geotiff is to allow the definitive identification of georeferenced locations within a raster dataset.  | <ul><li>In widespread use worldwide<li>strong software support in the form of the open source libgeotiff library and Geospatial Data Abstraction Library (GDAL) package. <li>Many commercial GIS and spatial data analysis software products support reading and writing GeoTIFF data. <li>The Earth science cloud computing community is developing a means of optimizing GeoTIFF files for use in cloud computing workflows. Cloud Optimized GeoTIFF (COG) files adhere to the GeoTIFF specification so all prior software and workflows can consume COG files.  </ul> | <ul><li>Discussion about how to increase interoperability.<li>GeoTIFF is not necessarily suitable for every data type. There are other scientific file formats that are well established within the NASA community, e.g., HDF5 and netCDF, that are approved for use in NASA Earth science data systems <li>GeoTIFF is not suitable for storing complex multi-dimensional data structures nor for storing vector data with many attributes or topology information </ul>| 
|**Zarr** | Zarr is a format for the storage of chunked, compressed, N-dimensional arrays. Uses HDF5 functionality but with increased flexibility| <ul><li>Create N-dimensional arrays with any NumPy dtype.<li>Chunk arrays along any dimension.<li>Compress and/or filter chunks using any NumCodecs codec.<li>Store arrays in memory, on disk, inside a Zip file, on S3, …<li>Read an array concurrently from multiple threads or processes.<li>Write to an array concurrently from multiple threads or processes.<li>Organize arrays into hierarchies via groups.</ul> | -----|