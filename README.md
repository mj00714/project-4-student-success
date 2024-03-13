# project-4-student-success

### Overview
Choosing the right education program can be a daunting task. There are thousands of post-secondary institutions in the United States alone and each seeks to attract new students through marketing and published rankings. Colleges and universities will often advertise the merits of their programs but, when comparing, most students want to understand which schools will provide the best return on their investment.

The goal of our project is to broadly analyze the college market and provide a ML model that offers insight into colleges and universities effect on post-graduate earnings. To do this, we’ll utilize the data.gov college scorecard. It’s a rich dataset that provides detailed metrics. We’ll utilize skills we’ve developed over the past ~20 weeks to create a ML model that can be used to predict the earnings of graduates.

Every college offers a different experience. From specialized programs, to geographic proximity to high-paying industries/sectors each school offers a unique characteristics that can help students secure the highest paying jobs after graduation. We wanted to look at the features of colleges of these universities to better understand the individual characteristics that drive earning potential. 

To understand the data, we plan to use a multiple linear regression model from scikitlearn. This will help us understand the variables that weigh into a student's income earning potential. 

### Discovery
Data.gov maintains a higher education scorecard dataset that contains detailed information on institutions, student demographics and academic performance. We gravitated toward this scorecard/dataset because it is a comprehensive view of the higher education landscape. Each scorecard contains over 200MB of data and there is a supplemental data dictionary that clearly defines the tables. For this analysis, we'll use the institution scorecard.

### Data Preparation
Rather than linking to the data.gov site, we're going to upload and compress the institution scorecard so we're working with a static dataset. We'll remove some unnecessary columns to reduce the file size (under 25MB) but will mostly leave the dataset intact.

Next, we'll identify the feature variables. We'll select fields that we feel are relevant to the overall academic experience and contain a mix of data types. Our initial list of features was approximately 80 variables. This was too many to use in the model but served as a good starting point. 

At this point, we decided that our target variable would be the field "Median Earnings of Independent Students Working and Not Enrolled 6 Years After Entry." We chose this as our target because it was a middle-of-the-road metric that would summarize the data appropriately. We discussed using a field that targeted the 90th percentile or mean of earnings but ultimately landed on the median earnings, 6 years after initial enrollment because it would apply to most students. 

### CSV Extraction / Database Ingestion

Because of the size of the data, we elected to read the data into Spark, as a starting poing. We created a simple script to read in the unzipped csv file and create a pyspark dataframe. We used this, along with the accompanying data dictionary to refine our original list. 

### Cleaning, Transformating and Loading to Pandas
Since we're leveraging a linear regression model, our feature list needs to be numeric data. Each column will weigh on the model so it's best if the data is comprised of continuous variables. We used this criteria to eliminate our first set of fields. 

Next, we looked at columns and rows that contained missing data. We found two main categories of missing data: "null" and "privacy suppressed" values. We used for loops to list/visualize the columns that would be least useful and, again, made another round of cuts to the feature list. 

We were now left with approximately 30 columns that could provide value to our analysis. We used the .corr method (comparing it to our target variable) to establish a baseline of relatedness to the income target variable. Not surprisingly, metrics related earning- before and after the 6-year mark- were the most correlated. That said, we observed relatively strong correlations in other metrics and proceeded to create the model. 

### Model Creation, Training and Optimization
Now the fun part- we were ready to create our multiple linear regression model. Using the further reduced feature set we used the new Pandas dataframe to:
1. Separate the features from target variable
2. Import the necessary libraries from sklearn
3. Split the data into training and testing data
4. Create the standard scaler
5. Fit/train the model
6. Score the model's accuracy

We had to run the model 10-15 times to fully optimize it. During this process, we had to go back and add some features. We struggled to get the model over 70% and had to revisit the data dictionary to identify new features. Eventually, we were able to acheive a r-squared score of 83.3%. 

### Findings and Conclusion
Unsurprisingly, the data that had the strongest correlation to the Earnings 6 Years After Initial Enrollment were other earnings metrics, before and after the 6-year mark. Those fields had correlations above 80%. That said, the other features included in our model had meaninful impact on the model. Some examples include:
* The highest degree offered at the institution
* The average students' age of entry (negative correlation)
* The median amount of debt a student takes on
* The cost of the program

As with any dataset, there are are factors outside of the data that play into how effective an institution is on a student's earning potential. A school can provide an alumni network in high-paying industries or have a recruiting pipeline that places students into lucrative jobs after graduation. 
