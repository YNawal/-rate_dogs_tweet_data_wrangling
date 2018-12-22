# WeRateDogs tweet data wrangling

# Desription

Analyzing data before wrangling and organizing it is a waste of time and effort.  In this repot, I will describe the work I have done by wrangling tweet archive of WeRateDogs (@rate_dogs).
The process takes place in 3 steps 
1.	Gather data
2.	Access data
3.	Clean data

# Process details


## 1.	Gather data 

The data we worked on were collected from three sources:

a.	Provided as a csv file:  'twitter-archive-enhanced.csv'

This file contains data extracted from @dog_rates user tweets. It contains basic tweet data (tweet ID, timestamp, text, etc.) for all 5000+ of its tweets as they stood on August 1, 2017.

b.	Provided as an url file:

url = 'https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv'

Using 'requests' package, I have downloaded the image-predictions tsv file, saved it in the current dirrectory, then load it as a pandas dataframe in the notebook.
What contains this file?
Each dog image posted with the tweet text are passed in different pattern recognition algorithms. The prediction coefficient as the pattern predicted of each algorithm (3) are gathered in a sheet and stored in tsv file.

c.	In order to gather more data related to our archive tweets, we used  tweepy library and tweet ids got from the first described file.
In this step, a tweeter API object is created and then used to gather tweeter data. As tweet data is stored in JSON format by Twitter, we used json package to write and read from and to a text file.


## 2.	Access data

Access our data is the second step. We can assess data for quality and tidiness using visual assessment by scrolling through the data in your preferred software application (Google Sheets, Excel, a text editor, etc.) and programmatic assessment by using code to view specific portions and summaries of the data (pandas' head, tail, and info methods, for example). Data quality dimensions are: completeness, accuracy, consistency and validity. In the section below, we report quality and tidiness issues in our data.

### Quality issues in our data:

#### Twitter archive data table (first data source)
* Missing values:

In retweeted_status_user_id, retweeted_status_timestamp, in_reply_to_status_id and in_reply_to_user_id  variables.
Note: We only want original ratings (no retweets) that have images. Then, we will not need retweeted_status_id, retweeted_status_user_id, and retweeted_status_timestamp anymore.).
Missing values is a quality issue, while remove columns is a tidness issue. I will deal with this point in quality section.

* Erroneous datatypes:
        * in_reply_to_status_id :        is a float not an integer
        * in_reply_to_user_id:          is a float not an integer
        * retweeted_status_id:           is a float not an integer
        * retweeted_status_user_id:      is a float not an integer
        * retweeted_status_timestamp:    is a string not a datetime
        * timestamp:                     is a string not a datetime

* rating_denominator variable has values <10.  Text tweets show errors when extrating 	these numbers.      
* There are four categories for source variable. there is some irrelevant text: html code.   
* One character or invalid name.
* Same dog with two stage: some values in doggo, floofer, pupper and puppo columns need to  be revised. 
* Values in doggo, floofer, pupper and puppo columns are bad represented.
* Null values are represented in the table sometimes by None and sometimes by NaN.

#### Image predictions data table (second data source)
* There are duplicate records.

#### Twitter extension data table (Third data source)
* type of tweet_id, favorite_count and retweet_count is string not integer.
* truncated column has one value: False.

### Tidiness issues in our data

#### Twitter archive data table (first data source)
* doggo, floofer, pupper and puppo column should be merged into on column: stage
* Rating values should be one column 

#### Image predictions data table (second data source)
* p1, p2 and p3 columns should be merged into two columns: prediction algorithms and breed prediction.
* p1_conf, p2_conf and p3_conf columns should be merged into one column: prediction coefficient.
* p1_dog, p2_dog and p3_dog should be merged into one column: is_a_Dog
* This table should be concatenated with twitter archive table.

#### Twitter extension data table (third data source)
* This table should be concatenated with twitter archive table.

## 3.	Clean data
In this step of wrangling data process, we implement the proposals listed in the Access section. The more precise and clearly the assessment, the more aisily Clean step will be.


# Files description
## Code files:
* wrangle_rate_dogs.ipynb: contains all action I have done during wrangling data process.
* wrangle_rate_dogs.htm:l an html version of the previous file
* analyse_rate_dogs_report.rmd: contains a slight analysis on cleaned data
* analyse_rate_dogs_report.html: an html version of the previous file
  
## Data files
* data/twitter-archive-enhanced.csv: contains tweet arche of @rate_dogs user.
* data/image-predictions.tsv: contains prediction result of the image posted in tweets.
* data/tweet_json.txt: a data extracted using tweepy library. Contain additional information of tweets stored in twitter-archive-enhanced file.
* data/twitter_archive_master.csv:  contains all previous cleaned and combined data.
 
