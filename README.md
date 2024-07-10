# lattice-design-compression
Predicting the design of 5 TPMS lattice structures using compression tests

I worked on this project during my master's thesis titled *Machine Learning Assisted Design of UV Curable Resin-based Lattice Structures for Additive Manufacturing* at the University of Regina. I'll first describe the problem I encountered and how I gathered the data. Then, I'll explain the methods I used to develop the prediction model.

## Project Description
This project investigates the use of machine learning to optimize the design of polymeric foams with improved mechanical properties for applications requiring deformation such as mattresses, shoe insoles, military helmets, and so on. Traditional polymeric foams, while widely used, suffer from limitations in their cell structure design.

This project utilizes lattice structures, a type of cellular material, to achieve superior mechanical performance. The project focuses on:

1. **Lattice Design:**  93 unique lattice unit cells were designed using five key parameters:
   - **Lattice Type:** Gyroid, Schwarz, Diamond, Lindinoid, SplitP
   - **Cell Dimensions:** X, Y, and Z-axis lengths
   - **Cell Wall Thickness**
2. **Fabrication:**  The designed lattice structures were fabricated using resin 3D printing.
3. **Mechanical Testing:**  Compression tests were conducted on the samples up to 50% height reduction, following the ASTM D3574-17 standard to generate stress-strain data.
4. **Data Collection:**  The testing process resulted in 76,761 observations with seven variables:
   - **Independent Variables:** Lattice Type, Force applied, Strain
   - **Dependent Variables:** X, Y, Z dimensions, Cell Wall Thickness

The project aims to develop a machine learning model that can predict the optimal unit cell dimensions (X, Y, Z, and thickness) based on the applied force, strain, and chosen lattice type.

## Installation
### Software Requirement
The codes were written with JupyterNotebook IPython 7.31.1 environment and Python programming language version 3.9.13. They were executed on a system setup comprising an 11th Generation Intel® Core™ i5 CPU with four cores and a clock speed of 2.40 GHz, together with 8.00 GB of RAM, operating on the Microsoft Windows 11 Home OS.

To implement the code and obtain the models for this project, ensure you have installed the necessary packages. Initially, descriptive statistics were implemented to understand the dataset and determine methods for achieving better modeling results. To begin, install the required packages by running the following command for the ["Descriptive Statistics"](https://github.com/javadho/lattice-design-compression/blob/main/Descriptive%20Statistics.ipynb) file:

`pip install pandas seaborn matplotlib scipy scikit-learn nump`

## Data Sources
The dataset has not been publicly released yet. I will upload it once it becomes accessible to everyone. However, you can see a portion of the raw dataset below for reference.

|Lattice Type |      X(mm)  |      Y(mm)  |  Z(mm)      |Thickness(mm)| Force(N)    | Strain(mm)  |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| SplitP      | 10.0        |      8.7    |      9.5    |      1.1    |      0.219  |      0.0001 | 
| SplitP      | 10.0        |      8.7    |      9.5    |      1.1    |      0.2675 |      0.0023 | 
| ...         | ...         |      ...    |      ...    |      ...    |      ...    |      ...    | 
| Gyroid      | 8.5         |      6.4    |      9.1    |      1.8    |    1068.057 |     14.4929 | 
| Gyroid      | 8.5         |      6.4    |      9.1    |      1.8    |    1068.731 |     14.5004 | 
