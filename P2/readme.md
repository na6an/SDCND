# Project 2: Traffic Sign Classification
This is the write-up report for project2 Traffic Sign Classification.

HTML file contains code exported from ipynb. (as required in submission instruction)  
Zip file contains images in html.

## I. Dataset Exploration
First of all, all cells in this section is combined into two cells as project developes to reduce the number of “shift + enter” for easier execution and used as an experimental debugging place.

### Dataset Summary & Exploratory Visualization
1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.  

<img src="https://github.com/na6an/SDCND/blob/master/P2/img/Picture1.png" alt="alt text" width="480" height="180">   
Above figures are the outcomes of following print format describe various datasets.  

<img src="https://github.com/na6an/SDCND/blob/master/P2/img/Picture2.png" alt="alt text" width="520" height="180">   
The number series “1 38 33 11 38 18 12” at the end is the class id of the sign images following.

<img src="https://github.com/na6an/SDCND/blob/master/P2/img/Picture3.png" alt="alt text" width="520" height="120">   


2. Include an exploratory visualization of the dataset.  
This image series is created with following “gallery” function to allow easier exploration of signs than simple matplotlib using subplot.   This function takes a 4D feature set (standard X feature we use in this project), first index number of desired image (fst_n), and the number of total images in series (n).


Keep in mind, there is a minor usability bug that first block is always black, filled with zeros.  
Also, it returns some dimension error sometimes.  
In that case, initial stack call statement has to be switched by commenting out/uncommenting.

One of the weird thing I noticed was, using this function, the training features in original data set appear to have series of similar signs. (I double checked the several times, make sure I did not corrupt it) Each of them were slightly different, but almost too similar to hardly notice the small variation. This makes me to suspect if the original was overwritten somehow.  

And the last graph is the number of sign counts in each class.  

In next cell, it returns index number of unique to each class, and randomly output one of signs.
