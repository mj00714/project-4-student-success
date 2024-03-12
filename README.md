# project-4-student-success

### Overview
Choosing the right education program can be a daunting task. There are thousands of post-secondary institutions in the United States alone and each seeks to attract new students through marketing and published rankings. Colleges and universities will often advertise the merits of their programs but, when comparing, it's often unclear which institutions are similar to one another.

The goal of our project is to broadly analyze the college market and provide a ML model that clusters colleges and universities. To do this, we’ll utilize the data.gov college scorecard. It’s a rich dataset that provides detailed metrics. We’ll utilize skills we’ve developed over the past ~20 weeks to create a ML model that can be used to associate academic institutions.

Our dataset is a scorecard of American universities provided by data.gov. To understand the data, we plan to use the Kmeans method to cluster universities, based on their scorecard KPIs.

### Discovery
Data.gov maintains a higher education scorecard dataset that contains detailed information on institutions, student demographics and academic performance. We gravitated toward this scorecard/dataset because it is a comprehensive view of the higher education landscape. Each scorecard contains over 200MB of data and there is a supplemental data dictionary that clearly defines the tables. For this analysis, we'll use the institution scorecard.

### Data Preparation
Rather than linking to the data.gov site, we're going to upload and compress the institution scorecard so we're working with a static dataset. We'll remove some unnecessary columns to reduce the file size (under 25MB) but will mostly leave the dataset intact.

Next, we'll identify the feature variables. We'll select fields that we feel are relevant to the overall academic experience and contain a mix of data types. For the purpose of the project, the feature list will be between 7-15 fields.

CSV Extraction / Database Ingestion

Our initial plan is to use MongoDB as our database. We’ll write a script to extract relevant columns from the csv file using methods we’ve practiced over the past few months. Once the data is in the MongoDB, we’ll use MongoCompass to examine the output.

Transformation and Load to Pandas
After cleaning the data and loading it into MongoDB, we’ll move it back into Jupyter notebooks to perform our analysis.

### Data Analysis
Once cleaned and reduced dataset is back in Jupyter, we’ll use our Kmeans method to perform analysis. The goal will be to create clusters that can help segment the universities.
