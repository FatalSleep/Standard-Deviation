# Standard-Deviation
In statistics the "standard deviation," is the average distance away from the mean. This is typically used to find the distribution of some dataset `K` away from the mean `M` where the range or distance from the mean per standard deviation varies by the density of the dataset.

This is useful if for example you wanted to find the average value between some data points where the average isn't skewed by points far outside the mean. Or if you wanted to check the density of some population relative to a precise location.

How to find the standard deviation:
```
// Define your variables: Where DataSet is a list of data points/values and everything is initialized to 0 (default).
DataSet, DataSize, Mean, SqrdSum, Variance, Deviation;

// Add up DataSet and the square of the DataSet:
loop(auto data in DataSet):
    Mean += data
    SqrdSum += sqr(data)

// Calculate the Mean, Variance and Deviation:
Mean  = Mean / DataSize
Variance = SqrdSum / DataSize - sqr(Mean)
Deviation = sqrt(Variance)
```
The `Mean` is just the average of the data set. The `Variance` expresses how clustered or dispered the dataset is from the mean (higher variance higher dispursion, lower variance, lower dispersion). The `Deviation` is the average distance of all data points away from the mean.
