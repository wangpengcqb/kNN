# kNN

Notes

The kNNScript.ipynb implements the k-NN model that avoids time leakage (default for k = 4). Need install jupyter and related packages to run the script. 

To avoid the time leakage, the simple implementation used here is to filter the training data which has earlier close date for every test sample. And then apply k-NN model from sklearn to the filtered training data.  

The Median Relative Absolute Error (MRAE) for test data (1% of the whole data size) is 0.239.

To find the optimal number k, we can run the model for a number k from 3 to 20 and check the Median Relative Absolute Error (MRAE) by using cross-validation. For each k number we perform cross-validation independently. The optimal k value should be the one with lowest RMAE value.

We plot the ARE vs the close time and spatial coordinates. For the time plot, the RAE tends to decrease with time. Especially after July 2015, the RAE becomes very low. More data is available as time goes on, providing a more accurate predicting model. For spatial plot, in the longitude around -100 and latitude 30 has the largest ARE. The price prediction is very sensitive to the geographical region of the training data. Much larger RAE is expected of the price prediction outside this geographical region in comparison to the RAE inside this geographical region.

The implementation is relative slow and computationally expensive. To improve this model, we can implement preprocessing to filter a large portion of data that are unlikely to match the target data for prediction. By doing this we can speed up k-NN model especially for large dimensions of feature space. 

To productionize this model, we can implement parallelization to k-NN model. To divide the test data into mini batches and for each batch apply the k-NN model parallely. And if the data is big we can apply apache spark or MapReduce on Hadoop to speed up k-NN model. 
