# PCA with Breash Cancer Dataset

In this project, I aimed to decrease the dimension of the dataset, by applying Principal Component Analysis technique.
I used just the most important 3 features to apply PCA in the dataset instead of using the whole dataset.

- First I chose the most important 3 features from a dataset by using domain knowledge,
- Then I applied dimensionality reduction technique, PCA, on the important features.

As a result, it shows that PCA can successfully reduce the dimension of these 3 important features while
the first and the second eigenvectors cover %98 of the variability of the data in total.

# Dataset

I used a dataset called “Breast Cancer Wisconsin (Diagnostic) Data Set” at Kaggle.

The dataset is collected from the patients from University of Wisconsin Hospital as microscopic FNA images in 1995. Dataset characteristic is multivariate. The Kaggle challenge is for predicting whether the cancer cell is benign or malignant.

Features in this dataset describes the nuclei characteristics of the FNA microscopy images.
There are columns for the information, ID and diagnosis. The diagnosis column has two distinct values M (for malignant) and B (for benign) which shows the diagnosis of the breast tissues.

Here are main features obtained from cell nucleus:
- radius (mean of distances from center to points on the perimeter)
- texture (standard deviation of gray-scale values)
- perimeter (size of the core tumour)
- area
- smoothness (local variation in radius lengths)
- compactness (perimeter^2 / area - 1.0)
- concavity (severity of concave portions of the contour)
- concave points (number of concave portions of the contour)
- symmetry
- fractal dimension ("coastline approximation" - 1)

There are other features calculated from the mean, standard error and worst (mean of the largest tree values) values from the main features above. In total, the dataset has 30 features.

In total the dataset has 569 data points with 30 features. It means that we will have 30 dimensions if we use all the features in our study.

![Figure 0, class count](https://github.com/Ozgedp/PCA-with-Breast-Cancer-Dataset/blob/master/images/1Data_count.png)  

Figure above shows the amount of the data that has been classified as malign and benign in our dataset. We can see that there is an imbalance between classes.


# EDA and Choosing Important Features

Fine needle aspiration (FNA) is one of the most important and effective technique to diagnose breast cancers. With this technique, a sample tissue is taken from patients’ breast lumps by using a thin needle. After that the sample is air-dried as a thin layer, stained with specific dyes to see nucleus better and then images are observed under a microscope.

![Figure 1, Output](https://github.com/Ozgedp/PCA-with-Breast-Cancer-Dataset/blob/master/images/3malign_benign.png)  

Figure 1. Fine Needle Aspiration images of breast samples. a) from a benign tumour (non-cancerous) b) from a malign (cancerous) tumour [3].

Figure 1 shows an example image of FNA microscopy. There are some differences between the pyhsical features of benign and malign cells, especially in their nucleus. For example, the malign cell nuclei can be large and irregular shaped compare to benign cells [4]. It is not easy to recognise the difference between these samples, it requires experts to differenciate.

Also a study showed statistically significant differences between benign and malign cell nucleus features pyhsical such as perimeter, diameter, concave points, area, compactness of the nucleus [5].

There are some key features of this dataset. 
Malign cells are tend to have enlarged nuclei so that area, perimeter and radius features can be important features. At the same time, these features should be highly correlated to each other because they used to calculate each other. Thus one of these feature should be informative to show the distribution of this measurement. I will choose just area feature.

Concave points and compactness of the cell nuclei are also important features. I expect high correlation between concave point and concavity features so that we need to choose one of this. Concave point is found very informative in a paper as well [1] so that I will choose this feature.

Symmetry is also an important feature due to the asymmetric features of the malign nuclei. Texture of the image which shows gray scaled values should be informative to differentiate nuclei.

Mean and worst versions of these features are important metrics but they can be highly correlated, so that mean values of the features should describe it well. For example instead of “area_worst” feature we can choose “area_mean” feature.

Here is a correlation heatmap which shows that most if these features are highly positively to eachother. 

![Figure 1, Output](https://github.com/Ozgedp/PCA-with-Breast-Cancer-Dataset/blob/master/images/2_Correlation_heatmap.png)  


Finally, I expect higher numeric values for mean values of the area, concave points, compactness for malign cell nuclei compare to benign cell nuclei and I will choose only these features as the most important features for this classification problem. 

![Figure 1, Output](https://github.com/Ozgedp/PCA-with-Breast-Cancer-Dataset/blob/master/images/4_statistics.png)  

Table above shows descriptive staistics of choosen features which give us an idea about how these features are dispersed. From the table, while the maximum value of area_mean is 2501, compacness_mean is 0.3454. It shows that all of these features needs to be standardized or normalized before applying PCA. 

# Univariate Analysis

# Bivariate Analysis

# Multivariate Analysis

# PCA Application

Explained variance ratios for the first principal component and second principal components are 0.815, 0.167 respectively. It shows that the first principal component explains 81% variance in our given three features. If we need more than 81% variance, we should also use the second component. First and second principal component together explains 98% variance of the given features. Thus, there is not much need to use three features. Instead, we can use the first and the second eigenvectors and cover 98% variance at the data. When we reduce the dimension, we will reduce the complexity of our model so that we can have better model performances.


