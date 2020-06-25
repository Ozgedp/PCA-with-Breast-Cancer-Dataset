In this project, I aimed to decrease the dimension of the dataset,by applying Principal Component Analysis technique.
I used just the most important important 3 features to apply PCA in the dataset instead of using the whole dataset.

- First I chose the most important 3 features from a dataset by using domain knowledge,
- Then I applied dimensionality reduction technique, PCA, on these features.

As a result, it shows that PCA can successfully reduce the dimension of these 3 important features while
the first and the second eigenvectors cover %98 of the variability of the data in total.

# Dataset

I used a dataset called “Breast Cancer Wisconsin (Diagnostic) Data Set” at Kaggle.

The dataset is collected from the patients from University of Wisconsin Hospital as microscopic FNA images in 1995. Dataset characteristic is multivariate. The Kaggle challenge is for predicting whether the cancer cell is benign or malignant, so that it is a classification problem.

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

# Univariate Analysis

# Bivariate Analysis

# Multivariate Analysis

# PCA Application

Explained variance ratios for the first principal component and second principal components are 0.815, 0.167 respectively. It shows that the first principal component explains 81% variance in our given three features. If we need more than 81% variance, we should also use the second component. First and second principal component together explains 98% variance of the given features. Thus, there is not much need to use three features. Instead, we can use the first and the second eigenvectors and cover 98% variance at the data. When we reduce the dimension, we will reduce the complexity of our model so that we can have better model performances.


