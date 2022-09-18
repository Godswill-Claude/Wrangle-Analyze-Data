# Wrangle-Analyze-Data


## Introduction

    This project required us to gather and wrangle the following three pieces of datasets: 

1. twitter_archived_enhanced.csv file (containing basic tweet archive of Twitter user @dog_rates, also known as WeRateDogs. WeRateDogs is a Twitter account that rates people's dogs with a humorous comment about the dog. These ratings almost always have a denominator of 10, while the numerators almost always have a value greater than 10.
   This archive contains basic tweet data (tweet ID, timestamp, text, etc.) for all 5000+ of their tweets as they stood on August 1, 2017. However, only 2356 of these tweets contain ratings, hence only 2356 records are contained herein in this dataset.

2. tweet_json.txt (Additional Data to be gathered by querying the Twitter API, containing the 3000 or so most recent tweets. This  dataset contains additional columns such as retweet count and favorite count - two of the notable column omissions in the twitter_archived_enhanced.csv).

3. image-predictions.tsv (containing a table full of image predictions (the top three only) of breeds of dogs in the WeRateDogs Twitter archive, alongside each tweet ID, image URL, and the image number that corresponded to the most confident prediction of breeds of dogs.

> Software packages used include: Python, pandas, numpy, matplotlib and a few other python libraries 

## Data Gathering
> The methods required to gather each piece of data are different. I took the following steps to gather each piece of dataset mentioned above for this project and load them in the jupyter notebook.

1. twitter_archive_enhanced.csv: WeRateDogs downloaded their Twitter archive and sent it to Udacity via email, which in turn was given to us students for this project. So, all I had to do was directly download to my local machine, after which I uploaded the dataset to my jupyter dashboard and finally read it into a pandas dataframe in the wrangle_act jupyter notebook template.


2. image-predictions.tsv: This file is present in each tweet according to a neural network and hosted on Udacity's servers. Hence, I used the Requests library and the following URL:https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv to download the dataset programmatically into the jupyter dashboard on my local machine. After which, I read the .tsv file into a pandas dataframe using appropriate coding. 

3. tweet_json.txt: The Twitter API requires authentication since it is not open-source. Hence, I first signed up for a twitter account, then set up a developer account with which I used to apply for and obtain my twitter API credentials (Consumer API keys, Access Token and Access Token Secret). Next, I used the code provided in the Getting started portion of the Tweepy documentation to create an API object which, with the help of Python's Tweepy library, was used to query the twitter API in order to gather Twitter data - containing each tweet's retweet count and favorite (or "like") count plus some other interesting fields/columns. Since we are dealing with a text file, I used appropriate codes to write each tweet's JSON data to its own line - line by line in steps. After which, each tweet's entire set of JSON data was then stored in a file called tweet_json.txt file.Then I used appropriate code statements to read this .txt file line by line into a pandas dataframe.

## Data Assessing

> In this section, I used both visual and programmatic assessments to detect and document nine (9) quality issues and three (3) tidiness issues, though the list is not exhaustive.

### Quality issues

#### df_3
1. The column name 'id' should be changed to 'tweet_id' for consistency with df_1 and df_2


#### df_1 (opened and visually inspected in excel spreadsheet application)
2. The columns: in_reply_to_status_id, in_reply_to_user_id, retweeted_status_id, retweeted_status_user_id, expanded_urls and retweeted_status_timestamp all contain missing (aka null) values (represented as NaN in pandas).

3. Some values/records under the column "name" show 'None' or 'a', which should not be


#### df_2
4. The columns: in_reply_to_status_id, retweeted_status, quoted_status_id, quoted_status_id_str, quoted_status_permalink and quoted_status all contain missing (aka null) values (represented as NaN in pandas). 
5. The datatype of the column/field created_at is not the correct format 
 
#### df_1
6. The columns doggo, floofer, pupper and puppo are in string formats instead of categorical formats

#### df_2
7. The columns p1, p2 and p3 are in string formats instead of categorical formats.
8. Inconsistency in casing for the columns p1, p2 and p3 (sometimes begin with a lowecase letter and other times uppercase)
9. Inconsistency in the number of decimal places in the columns p1_conf, p2_conf and p3_conf


### Tidiness issues

##### df_1
1. The columns doggo, floofer, pupper and puppo all need to be combined into a single column called dog_stage

##### df_1, df_2 and df_3
2. The .duplicated() method revealed duplicate columns like tweet_id (occurs in df_1 and df_2), 
    source, in_reply_to_status_id and in_reply_to_user_id (occurs in both dataframes 1 and 3), we will 
    need to determine how many datasets we actually need. Since the variables in all 3 pieces of 
    datasets all relate to the tweet archive of Twitter user @dog_rates, also known as WeRateDogs, all 
    three datasets should be conbined into one high-quality and tidy master pandas DataFrame. 

##### df_3
3. id and id_str contain exactly same values; so one of the columns should be removed

## Cleaning Data
> In this section, I cleaned all of the issues I documented above. 

> First, I made a copy of the original three datasets before I commenced cleaning. Next, using appropriate codes I began the cleaning operation from the first quality issue, then onto the three tidiness issues and finally I tackled the rest of the quality issues. The result was a high-quality and tidy master pandas dataframe, which I then stored as twitter_archive_master.csv
