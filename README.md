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

Let’s start with some univariate analysis. Figure 1 shows the scatter plots for the predictor versus the mean of the area or concave points or compactness features. There are some overlapping points between benign (‘B’) and malign (‘M’) cells so that it is not easy to distinguish. For example, in the graph titled ‘area vs diagnosis’, when we have a sample that the nucleus area ranges between 500 and 1000, we can not clearly say whether it is malign or benign.

![Figure XXX, Output](https://github.com/Ozgedp/PCA-with-Breast-Cancer-Dataset/blob/master/images/4_statistics.png)  

Figure 1. 2D Scatter plots for the important features ‘area’, ‘concave points’ and ‘compactness’ versus diagnosis. In diagnosis axis, ‘B’ shows benign samples as green circles, ‘M’ shows malign samples as red circles. It is evident that the only feature itself is not enough to differentiate categories; thus, it is a good idea to apply bivariate analysis. 

# Bivariate Analysis

Figure 2 shows scatter plots by using every combination of area, concave points and compactness and coloured by the diagnosis of the categories.

Figure 2. Pair plots compares probability density functions and scatter plots for chosen features coloured by their category.

I used density plot (a continuous form of a histogram) in the diagonal graphs instead of histogram because at the histogram it was not easy to distinguish overlapping frequencies.

From Figure 2, we can see that we can better distinguish the points for classes when we used two important features. The diagonal graphs show the distribution of malign and benign sample values by feature. Each class have a different distribution, and none of them shows us normal distribution; thus, it might be challenging to generalize by statistical models.

At Figure 2, most of the cases the distributions are slightly right-skewed, it states that most of the malign cases mean of the concave points are around 0.1, and the number of malign cases decreases when we have concave points mean value more than 0,1. The distribution states that for malign samples, nucleus area, compactness and concave points are more likely to be larger than benign samples, which is expected.

As a result of the distribution of the graphs, we might do log transformation to have a distribution close to Gaussian Distribution. Area feature has values between 143 and 2501, while compactness and concave points values are between 0 and 1. Thus, we can have a logarithmic transformation for just “area” feature.

From Figure 2, we can also get a general idea about pairwise correlation for the chosen features. When we look at scatter plots, all of our features are positively correlated with each other. For example, if we look at the scatter plot on the top right corner of Figure 2, we can see that while area increases, the number of concave points also increases.


# Multivariate Analysis

At the same time, there are some overlapping areas so that increasing dimension might give us better results. We can do a multivariate analysis by using all three predictors as a dimension.

Figure 3. 3D scatter plot for features ‘area’, ‘concave points’ and ‘compactness’, coloured by diagnosis. Green circles show benign samples, red circles show samples malign samples.
In figure 3, all the features are normalized by using Z score. Before normalization the range of the area was between 143 and 2501, and no it is between 5 and -2. This normalization results better scaled graph and can give us better performance when we use a statistical model to make prediction.
Although there are some overlapping areas in the Figure 3, using three features increases the separation between classes and it can give us better prediction accuracies compare to bivariate analysis.


# PCA Application

I first standardized the dataset, and applied PCA. Figure 4 shows the plot of the obtained eigenvectors.
Here is the code for PCA and the plot for 1st eigenvector vs 2nd eigenvector.

Figure 4. Graph of first eigenvector versus second eigenvector. The graph coloured by classes, yellow circles shows ‘Benign’ classes, blue circles shows ‘Malign’ classes.

Explained variance ratios for the first principal component and second principal components are 0.815, 0.167 respectively. It shows that the first principal component explains 81% variance in our given three features. If we need more than 81% variance, we should also use the second component. First and second principal component together explains 98% variance of the given features. Thus, there is not much need to use three features. Instead, we can use the first and the second eigenvectors and cover 98% variance at the data. When we reduce the dimension, we will reduce the complexity of our model so that we can have better model performances.

When I print the principal components, it returns 2 x 3 matrix. The first row shows the first eigenvector, the second row shows the second eigenvector. Here is the code that outputs eigenvectors.

To understand the correlation between eigenvectors and the features, we can have a look at the correlation heapmap at Figure 5.
Here is the code to plot correlation heatmap for eigenvectors and predictors.

Figure 5. Correlation heatmap for eigenvectors versus predictors
At Figure 5, it is not easy to understand which feature has the most effect on eigenvectors, but we can say that while the first eigenvector is positively correlated to each predictor, the second eigenvector has mixed correlation with predictors.


