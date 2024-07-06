# lattice-design-compression
Predicting the design of 5 TPMS lattice structures using compression tests

I, Javadhoo, worked on this project during my master's thesis titled *Machine Learning Assisted Design of UV Curable Resin-based Lattice Structures for Additive Manufacturing* at the University of Regina. I'll first describe the problem I encountered and how I gathered the data. Then, I'll explain the methods I used to develop the prediction model.

## Problem Statement

Polymeric foams are widely used in many industries because of their excellent qualities. Compressing these foams is important for making products lighter, so it's crucial to optimize how they deform for each use. However, designing the cell structures of foams has been a challenge. Recently, this issue was addressed by using lattice structures instead. These lattice structures can improve mechanical properties and open up new uses, especially in products needing a lot of deformation, like mattresses, shoe insole, military helmets, and so on.

## Data Preparation

Using real-world data for machine learning has benefits, even though it requires time and money. It captures the complexity and variety of actual data and handles unknown variables, making models more robust. At first, the lattice structures were created by designing and slicing, then fabricating them with a resin 3D printer. Compression tests were conducted next to generate stress-strain curves for each sample and to get the values of forces and their corresponding displacements.
