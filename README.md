# Standard-Deviation
In statistics the "standard deviation," is the average distance away from the mean. This is typically used to find the distribution of some dataset `K` away from the mean `M` where the range or distance from the mean per standard deviation varies by the density of the dataset.

This is useful if for example you wanted to find the average value between some data points where the average isn't skewed by points far outside the mean. Or if you wanted to check the density of some population relative to a precise location.

How to find the standard deviation:
```
// Where DataSet is a list of data points/values, DataCount is the size of DataSet.
// Everything else is initialized to 0 (default).
variables: DataSet, DataSize, Mean, SqrdSum, Variance, Deviation

// Add up DataSet and the square of the DataSet:
loop(for each `data` in DataSet):
    Mean += data
    SqrdSum += sqr(data)

// Calculate the Mean, Variance and Deviation:
Mean  = Mean / DataSize
Variance = (SqrdSum / DataSize) - sqr(Mean)
Deviation = sqrt(Variance)
```
The `Mean` is just the average of the data set. The `Variance` expresses how clustered or dispered the dataset is from the mean (higher variance higher dispursion, lower variance, lower dispersion). The `Deviation` is the average distance of all data points away from the mean.

When calculating the Standard `Deviation` or `Variance` you get a formula of `SquaredSum / DataSize - sqr(Mean)`. However, the `DataSize` also denoted as `N` can change to `N  -1` based on the type of measurement (population vs sample) to adjust for bias--this is Bessel's Correction. See the following for more information: https://www.uio.no/studier/emner/matnat/math/MAT4010/data/forelesningsnotater/bessel-s-correction---wikipedia.pdf
