# Definition
Mathematical science to collect, organize and analyze the data in such a way that one can draw meaningful conclusions from them.

# Data
Facts or pieces of information that can be stored, measured and retrieved.

## Ways to collect data
- Portal
- Surveys
- Experiments
- From customers through ratings and reviews

## Ways to organize data
- Databases - SQL, NoSQL
- Spreadsheets - Excel, Google Sheets

## Tools to Analyze data
- NumPy
- Pandas
- Matplotlib
- Seaborn
- Scikit-learn
- TensorFlow
- PyTorch

# Uses of statistics
- Weather forecasting
- Sports Analytics
- Election campaigns
- FMCG companies/ E-commerce companies (FMCG - Fast Moving Consumer Goods)
- medical, genetic research, pharmaceuticals

# Types of statistics
- Descriptive statistics(Describe) - Organize, summarize and complete data/population.
- Inferential statistics(Infer) - Use a sample to draw conclusions about a population.

# Techniques of descriptive statistics
- Measures of central tendency (mean, median, mode)
- Measures of symmetry (skewness, kurtosis)
- Measures of dispersion (range, variance, standard deviation, Interquartile range)

> Outliers are values that are significantly different from the rest of the data (Extreme values).
Mean, range, variance, standard deviation, skewness, kurtosis, covariance, and correlation are affected by outliers.

# Techniques of inferential statistics
- Estimation
- Hypothesis testing
- Regression analysis

# Sampling techniques
- Simple random sampling (Every member of the population has an equal chance of being selected in the sample)
    Disadvantages: Possibility of no member from a particular subgroup being selected in the sample.
- Stratified sampling (Divide the population into subgroups and then apply simple random sampling to each subgroup)
    Strata - subgroups
    Advantages: Ensures representation of each subgroup in the sample.
- Systematic sampling (Select members from the population at regular intervals)
    Every Nth member is selected in the sample.
- cluster sampling (Divide the population into segments/clusters and then apply simple random sampling to the clusters)
    Divide the population into clusters and then select some clusters at random and include all the members of the selected clusters in the sample.
> There are other sampling techniques like convenience sampling, snowball sampling, etc.

# Types of data

- Quantitative data (Numerical data)
    - Discrete data (Whole numbers). Ex: Number of students in a class.
    - Continuous data (Any value within a range) Ex: Height of students in a class.
- Qualitative data (Categorical data)
    - Nominal data (Categories with no inherent order) Ex: Gender, Marital status, etc.
    - Ordinal data (Categories with a natural order) Ex: Grades, Ratings, etc.
  
# Scales of date measurement.

- Nominal scale (Categories with no inherent order) (Pie chart, Bar chart)
- Ordinal scale (Categories with a natural order) (Pie chart, Bar chart, Line chart)
- Interval scale (Equal intervals between values but no true zero point) (Ex: Temperature in Celsius or Fahrenheit, Length, width, height, etc.) (Line chart, Histogram, Scatter plot)
- Ratio scale (Equal intervals between values and a true(compulsary and starting) zero point) (Ex: Weight, Height, Age, etc.)  (Line chart, Histogram).
    > Temprature can be negative, so it is not a ratio scale. But weight can't be negative, so it is a ratio scale.

# Descriptive statistics

summarization of data without modifying it at a specific time.

- Measures of central tendency (To find the single value that represents the wholde data)
    - Mean (Average)
    - Median (Middle value after sorting) (Avg of two middle values if even number of values)
    - Mode (Most frequent value) (Can be more than one)
  ### Python Implementation
  ```python
  impory numpy  as np
  data = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
  mean = np.mean(data)
  median = np.median(data)
  mode = np.mode(data) # Throws error. mode is not a function in numpy, use scipy.stats.mode

  from scypy import stats
  mode = stats.mode(data)

  import statistics
  mean = statistics.mean(data)
  median = statistics.median(data)
  mode = statistics.mode(data)
  ```

- Measures of dispersion (To find the spread of the data from the central tendency)
    - Range (Difference between the largest and smallest values)
    - Percentage (Related to 100)
    - Percentile (Value below which certain percentage of  observations falls)(Ex: 90th percentile is the value below which 90% of the observations fall)
    - Quartile (Divides the data into four equal parts)(Ex: 1st quartile is the value below which 25% of the observations fall and so on). There are 3 quartiles. Q1, Q2, Q3. Q2 is the median. Q1 = (n+1)/4 if totla numbers(n) are odd, Q1 = (n/4) if total numbers(n) are even. If Q1 is not an integer, then it is the average of the two middle numbers. Q3 = 3*(n+1)/4 if total numbers(n) are odd, Q3 = 3*n/4 if total numbers(n) are even. If Q3 is not an integer, then it is the average of the two middle numbers. Five point summary is the summary of the data using the minimum(Q0), Q1, median(Q2), Q3, and maximum(Q4) values.
    - Interquartile range (Difference between the 3rd and 1st quartiles. Used to detect outliers). Outliers always lie in Q0 and Q4. All values in Q1 and Q3 are considered normal. Outliers are values that lie outside the range of Q1 and Q3. (Box whisker plot is used to visualize the outliers. The box represents the interquartile range and the whiskers represent the range of the data. The outliers are represented by the points outside the whiskers)
    - Mean deviation (Average of the absolute differences from the mean)(Ex: If the date is 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, then the mean is 5.5. The absolute differences from the mean are 4.5, 3.5, 2.5, 1.5, 0.5, 0.5, 1.5, 2.5, 3.5, 4.5. The mean deviation is the average of these differences, which is 2.5 i.e on an avg each value is 2.5 units away from the mean)
    - Variance (Average of the squared differences from the mean) (Gives spread at an overall level and spread is directly proportional to the variance)
      - Population variance (Variance of the entire population)
        ```math
        \sigma^2 = \frac{\sum_{i=1}^{N} (x_i - \mu)^2}{N}\
    
        $\mu$ is the mean of the population and N is the population size.
      - Sample variance (Variance of a sample from the population)
        ```math
        s^2 = \frac{\sum_{i=1}^{n} (x_i - \bar{x})^2}{n-1}\
    
        $\bar{x}$ is the mean of the sample and n is the sample size.
        We use n-1 instead of n to correct for the bias in the sample variance. i.e the sample mean will be moved towards population mean.
        This is called Bessel's correction.
    - Standard deviation (Square root of the variance. Since variance is squared, standard deviation is the square root of the variance to get the original units to know how spread out the data i). We can know in which standard deviation the data point lies. i.e 1 standard deviation away, 2 standard deviations away, etc.
- Measures of shape
    - Skewness (Asymmetry of the distribution)
    - Kurtosis (Peakedness or flatness of the distribution)
- Measures of association
    - Covariance (Measure of how much two variables change together)
    - Correlation (Measure of the strength and direction of a linear relationship between two variables)
  

> Imputation is the process of replacing missing data with mean if there are no outliers, median if there are outliers, or mode if there are multiple outliers.



