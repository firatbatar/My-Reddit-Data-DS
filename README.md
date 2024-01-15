# My Reddit Usage Data Analysis

## Description

Sabanci University CS210 Introduction to Data Science Course Fall 2023-2024 Term Project.  
This project will be an analysis on my own <a href="https://www.reddit.com/" target="_blank">Reddit</a> usage.

## Table of Contents
**[Motivation](#motivation)**  

**[Tools](#tools)**  

**[Data Source](#data-source)**  
* [Requested data](#requested-data)
* [Reddit API](#reddit-api)

**[Data Processing](#data-processing)**

**[Data Visualizations](#data-visualizations)**

**[Data Analysis](#data-analysis)**
* [Active Times](#active-times)
* [My Votes on Reddit](#my-votes-on-reddit)
* [The Type of My Activity on Reddit](#the-type-of-my-activity-on-reddit)
* [Score of Comments and Ownership of Their Parent Posts](#score-of-comments-and-ownership-of-their-parent-posts)


**[Findings](#findings)**
* [Daily Activity](#daily-activity)
* [My Votes on Reddit](#my-votes)
* [The Type of My Activity on Reddit](#type-of-my-activity)
* [Score of Comments and Ownership of Their Parent Posts](#score-of-comments)  

**[Limitations](#limitations)**  
* [Data Sourced Limitations](#data-sourced-limitations)
* [Personal Limitations](#personal-limitations)

**[Future Work](#future-work)**  

## Motivation

While thinking about a project I thought I might analyze my interaction with the outside world which is done mostly through social media. Since Reddit is my primary social media platform, I decided to go with that.  
The motivation of this analysis is to gain a deeper understanding of my own Reddit usage patterns. By analyzing the subreddits I am subscribed to, when I am active on Reddit, and my engagement with posts and comments, I aim to gain insights into my online behavior and interests.

### Tools

**[Jupyter Notebook](https://jupyter.org/):** Used for coding and documentation.  
**[Pandas](https://pandas.pydata.org/):** Used for data cleaning, filtering, and structuring.  
**[Altair](https://altair-viz.github.io/index.html):** Mainly employed for exploratory data analysis (EDA) and interactive visualizations.  
**[Matplotlib](https://matplotlib.org/) and [Seaborn](https://seaborn.pydata.org/):** Supplementary for visualizations if needed.  
**[Numpy](https://numpy.org/):** Used for mathematical operations.  
**[Scipy](https://www.scipy.org/):** Used for statistical analysis.  
**[distfit](https://github.com/erdogant/distfit)** Used for distribution fitting.

## Data Source

I have two main sources of data:

-   Data that is directly exported from Reddit as a personal [data request](https://www.reddit.com/settings/data-request).
-   Data that is scrapped using [Reddit API](https://www.reddit.com/dev/api/) through a simple Python script using [PRAW](https://github.com/praw-dev/praw) package, following [Reddit's API rules](https://github.com/reddit/reddit/wiki/API). Script is available in `reddit_api_scraping.py` file.

In addition to these two, in order to create a general content type system for subreddits, I have created a Google Form to get "tags" annotated by hand. I wrote a Google Apps Script to automatically create a Google Form automatically from the data. Form is available [here](https://forms.gle/cKnMTpAyFxGkHKVy5). I have collected **7** responses from my friends. I have basically selected the most common tags three tags for each subreddit, but I have applied some more filtering. For details, see `reddit_api_scraping.py` file.

The final preprocessed data can be found in [`data`](/data/final_data/) folder.

### Requested data

Requested data is in .csv format and contains:

-   **Subscribed subreddits:** Bascially the subreddits that I am subscribed to.
-   **Login history:** Date, time, and IP address of my logins.
-   **Voted posts and comments:** Id, url, and the direction of my votes (upvote or downvote) for posts and comments that I have voted.  
-   **Created posts and comments:** Id, url, creation date, subreddit, and the ip of the device that I have created posts and comments. Comments also include the id of the post that they are created under.  

### Reddit API

Using Reddit API, I scrapped the following data:

-   The score (net upvotes) for each post and comment that I have voted.
-   The score of each post and comment that I have created.
-   The same script also combines annotated data with the raw data.

Requested data is read by scraper script and after scrapping, it is saved as new .csv files.  

Then the data is processed in `data_process.ipynb` file. The process includes cleaning and structuring the data. For details on every step for each different group of data, see the mentioned file.  

## Data Processing

The requested data and the scrapped data include many unused information and also some information that needs to be preprocessed. For all the details on the data processing, see `data_process.ipynb` file. But here is a summary of the process:  

- **Subreddits:** This data also holds followed users, so I have dropped them. Also, during scraping available flairs and annotations are added to the data. 
- **Login History:** The raw date was in UTC, so I converted it to my local time and extracted the day name. Also IP addresses are removed.  
- **Voted Posts and Comments:** I basically needed the URLs and the IDs to compare with other data, but did not needed themselves. So, I have extracted the subreddit name, checked if the subreddit is subscribed or not, and what is the score of the post/comment (if it is available) and made vote direction an integer. I have dropped the every other column.  
- **Created Posts and Comments:** Similar to the previous one, I have extracted the subreddit name, checked if the subreddit is subscribed or not, and what is the score of the post/comment (if it is available). I have dropped the every other column. Additionally, for comments, I checked if I was the owner of the parent post that the comment is created under.  

## Data Visualizations

Almost all the visualizations, the ones that are specific to an analysis are not here, are made in `data_visualization.ipynb` file. During the EDA, I have created many visualizations to understand the data better and to come up with interesting questions. Not all the visualizations are used and included in the final report. However, all can be found in the notebook. (If they are not visible for some reason they are also in the [figures folder](/figures/img/))  

I have used Altair for most of the visualizations. I have used it because it is very easy to use and very powerful, I wanted to create all my visualizations interactive so that EDA and final report is more clear and interesting.

## Data Analysis

All the analysis is done in `data_analysis.ipynb` file. Notebook is structured and commented in a way that it can be followed easily. In addition to the statistical tests, the notebook also includes some of the visualizations that are used in the report. Again (almost) all the visualizations are made using Altair so they are interactive. The final report is in its [own website](https://firatbatar.com/reddit-usage-analysis).  

### Active Times
I tried to look at my active times on Reddit to see if there is any pattern. I have looked at the days of the week and the hours of the day. Compared different days and hours to see if there is any difference. And also looked at how they compare to my school schedule.

### My Votes on Reddit
I wanted to what can affect my voting behavior. I have looked at the score of the posts and comments that I have voted and also the type of the subreddit that they are in. I used the tags that I have created using human annotators to classify the subreddits. 

### The Type of My Activity on Reddit
To see if my general interaction behavior is affected by what and how, I have looked to subreddits, their tags, and my subscription status. 

### Score of Comments and Ownership of Their Parent Posts
I wanted to see if the score of my comments is affected by whether I am the owner of the parent post or not. I have looked at the score of my comments and the ownership of the parent post.

## Findings

_For the detailed findings, please visit the [report](https://firatbatar.com/reddit-usage-analysis)._

### <a id="daily-activity" href="https://firatbatar.com/reddit-usage-analysis/analysis/logins/" target="_blank">Daily Activity</a>
- During weekdays I am more active on Reddit during the class hours, except for wednesdays and thursdays.
- During weekends I am more active on Reddit in the afternoon.

### <a id="my-votes" href="https://firatbatar.com/reddit-usage-analysis/analysis/myvotes/" target="_blank">My Votes on Reddit</a>
My votes are,
- mostly upvotes,
- not affected by the score of the post/comment,
- affected by the type of the subreddit.

### <a id="type-of-my-activity" href="https://firatbatar.com/reddit-usage-analysis/analysis/votedandcreated/" target="_blank">The Type of My Activity on Reddit</a>
My behavior on Reddit, interact with others via voting or creating content, is 
- affected by the subreddits,
- affected by the type of the subreddit,
- not affected by whether I am subscribed to the subreddit or not.

### <a id="score-of-comments" href="https://firatbatar.com/reddit-usage-analysis/analysis/commentscoreownership/" target="_blank">Score of Comments and Ownership of Their Parent Posts</a>
The amount of interaction with my comments is not affected by whether I am the owner of the parent post or not.

## Limitations

The limitations can be generally separated into two categories:

### Data Sourced Limitations

**Data Completeness:** Considering my time on Reddit and the way I interact with data is somewhat limited, the data stays a bit short for some of the possible analysis.  
**Subjectivity:** Like I have stated, Reddit does not have a native system to classify subreddit. Even though I tried to solve this using human annotators, they may have subjective biases affecting the accuracy of subreddit tags.

### Personal Limitations

**Privacy:** Since the project is based on a personal data, I have to be careful about the privacy of the data. There were some details that I did not want to share, so I did not use them in the analysis.  
**Knowledge:** Especially in the first stages of the project, I did not have enough knowledge about data science and data analysis. So, even though I tried to improve the project and the analysis as I learned more, there are still some parts inherited from the early stages of the project and some parts that I could not improve. With more knowledge and experience, and some knowledge about machine learning, I believe the project can be improved.

## Future Work

**Longitudinal Analysis:** Since data is on my usage of a social media platform, the analysis can be updated with newer data over a more extended period to observe changes in behavior and interests over time.  
**Advanced Analysis Techniques:** With more knowledge and experience on data science and machine learning, if I continue to take courses on the subject, I might return and improve some things that I am not able to do now.  
**Final Report Website:** I have created a website for the final report. However, due to my limited knowledge especially on using Altair, I could not create the website as detailed as I wanted and combine with interactive visualizations. I believe there is some room for improvement there.  