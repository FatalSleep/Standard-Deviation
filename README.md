# Fast-Standard-Deviation
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
The `Mean` is just the average of the data set. The `Variance` expresses how clustered or dispersed the dataset is from the mean (higher variance higher dispersion, lower variance, lower dispersion). The `Deviation` is the average distance of all data points away from the mean.

When calculating the Standard `Deviation` or `Variance` you get a formula of `SquaredSum / DataSize - sqr(Mean)`. However, the `DataSize` also denoted as `N` can change to `N  -1` based on the type of measurement (population vs sample) to adjust for bias--this is Bessel's Correction. See the following for more information: https://www.uio.no/studier/emner/matnat/math/MAT4010/data/forelesningsnotater/bessel-s-correction---wikipedia.pdf

The article above notes that `Bessel's Correction` introduces a lower bias due to using `sqrt()` for calculating the Standard Deviation, by calculating the square of the mean in-post when determining the Variance this error is adjusted out when compared to traditional calculations for variance and standard deviation.

----
# Polar Coordinate Standard Deviation
Unlike the above, I have no idea how this works. However it takes an input set of polar data (such as angles, hues, etc.) and finds the standard deviation then identifies outliers.
```C
#include <stdio.h>
#include <math.h>

const float PI2 = 6.2831853071795864769252867665590;
double atan2r(double _Y, double _X) {
	return fmod(atan2(_Y, _X) + PI2, PI2);
}

double raddiff(double _A, double _B) {
	return atan2(sin(_A-_B), cos(_B-_A));
}

int main() {
	double pi2 = 6.28318530718;
	double pixels[25] = {
		1.0, 0.9345, 0.76845, 0.8493, 0.0, 0.0, 0.95, 0.0, 0.0, 0.0, 0.0, 0.0,
		0.9345, 0.76845, 0.8493, 0.85, 0.85, 0.95, 0.85, 0.85, 0.85, 0.85, 0.85,
	};
	for (int i = 0; i < 25; i++) {
		printf("HUES(%d): %.6f\n", i, pixels[i] * PI2);
		pixels[i] = pixels[i] * PI2;
	}

	double kcos[25] = {0}, ksin[25] = {0};
	double meanx = 0.0, meany = 0.0;
	double high = 0.0, low = 1.0;

	for (int i = 0; i < 25; i++) {
		kcos[i] = cos(pixels[i]);
		ksin[i] = sin(pixels[i]);
		meanx += kcos[i];
		meany += ksin[i];

		if (pixels[i] > high) high = pixels[i];
		if (pixels[i] < low) low = pixels[i];
	}

	meanx /= 25.0;
	meany /= 25.0;

	double meanangle = atan2r(meany, meanx);
	double rvalue = (meanx * meanx) + (meany * meany);
	double klength = PI2 / (high - low);
	double deviation = sqrt(-2.0 * log(sqrt(rvalue) / klength));

	printf("\n\nPI2: %f\n", PI2);
	printf("MEAN(x,y,c): %.6f, %.6f, %.6f\n", meanx, meany, meanangle);
	printf("Standard Deviation: %.6f\n\n\n", deviation);
	
	for(int i = 0; i < 25; i++) {
		float diff = fabs(raddiff(pixels[i], meanangle));
		printf("Angle Delta: %.6f, %.6f, %s\n", pixels[i], diff, (diff > deviation)? "OUTLIER":"-------");
	}
	return 0;
}
```
