# lattice-design-compression
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

To implement the code and obtain the models for this project, ensure you have installed the necessary packages. Initially, Exploratory Data Analysis (EDA) were implemented to understand the dataset and determine methods for achieving better modeling results. To begin, install the required packages by running the following command for the [**EDA**](https://github.com/javadho/lattice-design-compression/blob/main/Exploratory%20Data%20Analysis.ipynb) file and also for the models' codes in the [**Prediction Models**](https://github.com/javadho/lattice-design-compression/tree/614c1bdcd45b8edd737942777cf30cfd7b110f03/Prediction%20Models) folder:

`pip install pandas seaborn matplotlib scipy scikit-learn nump`

For implementing the [**Graphical User Interface (GUI)**](https://github.com/javadho/lattice-design-compression/tree/614c1bdcd45b8edd737942777cf30cfd7b110f03/GUI) codes, you need to install additional packages as well. Run the following command:

`pip pillow`

## Data Sources
The dataset has not been publicly released yet. I will upload it once it becomes accessible to everyone. However, you can see a portion of the raw dataset below for reference.

|Lattice Type |      X(mm)  |      Y(mm)  |  Z(mm)      |Thickness(mm)| Force(N)    | Strain(mm)  |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| SplitP      | 10.0        |      8.7    |      9.5    |      1.1    |      0.219  |      0.0001 | 
| SplitP      | 10.0        |      8.7    |      9.5    |      1.1    |      0.2675 |      0.0023 | 
| ...         | ...         |      ...    |      ...    |      ...    |      ...    |      ...    | 
| Gyroid      | 8.5         |      6.4    |      9.1    |      1.8    |    1068.057 |     14.4929 | 
| Gyroid      | 8.5         |      6.4    |      9.1    |      1.8    |    1068.731 |     14.5004 | 

## Codes Structure

### 
The dataset was initially analyzed using [**EDA**](https://github.com/javadho/lattice-design-compression/blob/main/Exploratory%20Data%20Analysis.ipynb) to understand its structure and key characteristics. This included summarizing the data, checking for missing values, and generating summary statistics. Visualizations such as histograms, box plots, scatter plots, and correlation heatmaps were created to examine distributions, relationships, and potential outliers. Rank-Based Inverse Normal (RIN) transformation was used to normalize numerical variables.

The scatter plots and correlation heatmaps revealed slight correlations between force and Z, and a strong link between force and thickness, and force and strain. The box plots indicated that the lattice type variable is mostly independent of other variables, though there may be a very low relationship between lattice type and thickness.

### Prediction Models

To find the best models, categorical variables were converted to numeric using a label encoder, and the data was split into training and testing sets. Two machine learning techniques, Artificial Neural Networks (ANN) and Random Forest (RF), were utilized on the dataset, and their codes can be found in the [**Prediction Models**](https://github.com/javadho/lattice-design-compression/tree/614c1bdcd45b8edd737942777cf30cfd7b110f03/Prediction%20Models) folder.

**1. ANN:**
I employed TensorFlow and Keras frameworks to construct a neural network model and conducted hyperparameter optimization through Grid SearchCV with tuning Learning Rate, Activation Function, Batch Size, and Number of Epochs. The number of folds for Cross-Validation was set to 5.

**2. RF:**
The RandomForestRegressor function was employed, with MSE and R<sup>2</sup> being utilized as evaluation metrics. Hyperparameter tuning was conducted using Grid Search with 5-fold CV by tuning Maximum Depth and Number of Trees.

## Results and Evaluation
The selected metrics include R<sup>2</sup>, MSE, RMSE, and MAE. The RF algorithm significantly outperforms the ANN model. RF accounts for 79% of the variability in the target variable (R<sup>2</sup>), whereas ANN only explains 24%. Additionally, the MSE, RMSE, and MAE comparisons highlight RF's superior performance, with its predictions closely aligning with the actual values compared to ANN's results. This is also evident in the residual plots of these machine learning models.

### GUI
To make the model interactive, I used Tkinter for the GUI. In its code [**(RF_Model)**](https://github.com/javadho/lattice-design-compression/blob/a064b0afedf13e4377ad4b9edc7ee44547fed1b4/GUI/GUI_RF%20Model.ipynb), users can select from five lattice types (Diamond, Gyroid, Lidinoid, SplitP, and Schwarz) via a dropdown menu, revealing the corresponding cell shape. They can also input values for force and strain, with constraints visible by clicking the help button next to the force field. The RF model limits the strain range to 0-14.5 mm and sets a threshold of 600 Newton for force. Exceeding these ranges results in an error. By entering valid values and clicking predict, users can determine the X, Y, Z dimensions, and thickness of their lattice unit cell size.

![](https://github.com/javadho/lattice-design-compression/blob/main/RF%20Model.gif)

Additionally, I created a GUI for a specific application: designing lattice structures with different zones which is called Functionally Graded Lattices (FGL), each having distinct lattice designs. In the [**RF Model_FGL**](https://github.com/javadho/lattice-design-compression/blob/a064b0afedf13e4377ad4b9edc7ee44547fed1b4/GUI/GUI_RF%20Model_FGL.ipynb), users can specify the force and strain for the first and last zones and the number of intermediate zones. The GUI will then provide the values for X, Y, Z, and thickness for each zone, enabling a gradual and linear transition in lattice design.

![](https://github.com/javadho/lattice-design-compression/blob/main/RF%20Model_FGL.gif)

## Challenges
During this project, I encountered several challenges in predicting models. With 93 samples undergoing compression tests, each yielding around 760 force and strain values, there were multiple values for the same lattice type, X, Y, Z, and Thickness. Additionally, the initial force values for all samples were very similar. These factors complicated model prediction, making it difficult to use appropriate methods.

I considered adopting the Multiple Instance Regression (MIR) method, which suggests multiple bags containing several instances, closely resembling the dataset's structure. The collective assumption, where each instance's contribution to the targets is considered equal, aligns with this dataset. One approach was to calculate the mean force for each sample. However, the varying number of forces across samples and differences in failed samples could skew the results, rendering this method impractical.

## Publication
This research has been published in the 3D Printing and Additive Manufacturing journal on February 27, 2025. You can access the paper here: https://doi.org/10.1089/3dp.2024.0130. If you're unable to download it, feel free to contact me!

## Acknowledgments

I extend my deepest appreciation to [**Dr. Mohammad Khondoker**](https://www.linkedin.com/in/mahkhondoker?lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_contact_details%3B4wZ2dApeSrKGZjZsPtEGOg%3D%3D) for his remarkable guidance and support throughout this project at the University of Regina.
