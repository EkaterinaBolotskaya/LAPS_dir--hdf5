# LAPS_dir--hdf5

Data storage/exchange workflow for [LAPS project](http://verve.mit.edu/laps/)

## Project Overview

LAPS (funded by NSF Award# (FAIN): 1948453) project aims to facilitate the storage and exchange of laboratory data by providing a standardized format. 
We use a JSON file that contains information about the experiment, machine, the data obtained, etc. to organize and store experimental data.

The functions in this repository are designed to store and exchange laboratory data in a general format. 
They include the creation of an empty directory structure from a JSON schema, 
conversion of the populated directory to HDF5 format, and recreation of the original directory structure from the HDF5 file.

!!! Before running anything:

Go to the [LAPS project website](http://verve.mit.edu/laps/templates.html) to create a JSON schema file. 
You can either manually fill the form or use templates to generate the required .json file.
Save the created .json schema file to a location on your computer.

## Directory Contents
The project consists of four main functions:

### 1.1 **LAPS_1_empty_dir_create_delete.py** 
!!! This will DELETE your data!

   This function creates an empty directory structure based on the provided JSON schema file. 
   The directory structure will be created in an empty folder. 
   If this folder already exists, it will be DELETED (including all the data in it) and recreated.
   
### 1.2 **LAPS_1_empty_dir_create_update.py** 
   This function creates an empty directory structure based on the provided JSON 
   schema file (if the directory does not exist).  
   If this folder already exists, it will be UPDATED. The folders that exist, but no longer correspond to the .json structure
   will be deleted if empty and kept if not empty.

### 2. **LAPS_2_HDF5_from_directory.py** 
   This function converts the populated directory structure into HDF5 format for storage or exchange. 
   It requires the JSON schema file and the path to the populated directory. 
   The function will generate an HDF5 file, containing the data from the directory structure.
   
!!! Do not save the HDF5 into the directory containing the data. This will lead to recursive reproduction of the HDF5 every time you run the function.

### 3. **LAPS_3_create_directory_from_HDF5.py** 
   This function reproduces the original directory structure from the HDF5 file created in the previous step. 
   It requires the HDF5 file and specifies the output directory. 
   The function will recreate the directory structure and populate it with the data stored in the HDF5 file.

### 4. **LAPS_4_interactively_plot_timeseries.py** 
   This function selectively prints out fields from JSON schema file (original or recreated), 
   gets header arrays from there, downloads the time series data (path can be provided to original or recreated data), 
   and then interactively plots time series data.
   It requires the JSON schema file and .txt time series data file. 

### 5. **Main.ipynb** 
   Main scrpt to modify the paths and run the functions from.

### 6. **Test_input_output_data**
   An example folder with sample data and a sample JSON schema.

- `Paterson_Carrara_Test_2/`: A folder containing example data files. You can use this folder to create the HDF5.

- `Paterson5_CarraraTest.json`: A sample JSON schema file that defines the directory structure for the example data. You can create your own JSON schema [here](http://verve.mit.edu/laps/templates.html).

## Usage Instructions

![image](https://github.com/user-attachments/assets/da289927-c9a2-4e27-8c05-129ef481863e)

Follow the steps below to use the provided functions and manage your laboratory data:

1. Go to the [LAPS project website](http://verve.mit.edu/laps/templates.html) to create a JSON schema file. 
   You can either manually fill the form or use templates to generate the required .json file.
   Save the created .json schema file to a location on your computer.

2. Place Main.ipynb and the provided function files (`LAPS_1_empty_dir_create_delete.py`, `LAPS_1_empty_dir_create_update.py`, `LAPS_2_HDF5_from_directory.py`, `LAPS_3_create_directory_from_HDF5.py`, `LAPS_4_interactively_plot_timeseries.py`) 
   in the same directory (not necessarily where you want to manage your laboratory data).

3. Specify the path to the JSON schema file: schema_path. 
   This file defines the structure of the data to be stored. Specify the name for the empty directory to be created: empty_dir.
   
4. Run either version of **LAPS_1_empty_dir_create** function to create the initial directory structure based on the JSON schema. 
   This function will create an empty directory structure in a folder named empty_dir. 
   Please see comments above on the difference between the two versions if rerunning the function.

5. Populate the generated directory structure with your laboratory data. 
   You should organize the data according to the subfields defined in the JSON schema.
   If you want these scripts to be part of the HDF5, add them into the directory.

7. Specify the path to the populated directory: popul_dir (if you populated the original directory, the path should be the same as empty_dir).
   Specify the name for the HDF5 file to be created: hdf5_file.

8. Run the **LAPS_2_HDF5_from_directory** function to convert the populated directory structure into an HDF5 file. 
   This function will read data from the populated directory, generate an HDF5 file that represents the same structure, and dump the data there as binary files.

9. The HDF5 file can now be stored, exchanged, or used for further analysis. 
   You may choose to move it to a different location or share it with others.

10. To reproduce the original directory structure from the HDF5 file, specify the directory name: output_dir, 
   the file name for the recreated schema: recr_scdir, and the HDF5 file name: hdf5_file.
   Run the **LAPS_3_create_directory_from_HDF5** function. It will recreate the directory structure 
   and populate it with the data stored in the HDF5 file. The original JSON schema is recreated as well.

11. To interactively plot time series data from the recreated directory, 
    run the **LAPS_4_interactively_plot_timeseries** function. 
    This function requires the recreated JSON schema and the path to the time-series data (so modify the paths). 
    It will print selected fields from the JSON schema, get header arrays from there, and plot the time series data.

## Dependencies

Please ensure that you have the necessary dependencies installed to run these functions, 
such as the `h5py`, `json`, `numpy`, `openpyxl`, and `pandas` libraries. 
You can install them using a package manager like `pip`.

For any questions or issues, feel free to reach out. 

## Screenshots

- Folder structure to HDF5 file structure
  
![image](https://github.com/user-attachments/assets/94c171e6-c523-40aa-bfc2-6e3576287371)

- Interactive time-series data plotting
  
![image](https://github.com/user-attachments/assets/2c737463-45eb-4155-ac25-68d269bd576d)






