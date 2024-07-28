**Metrocar Funnel Analysis**

Metrocar is a (fictional) ride-sharing app - similar to Uber/Lyft.<br>
Our main goal is to perform a funnel analysis of our users to identify areas for improvement and optimization.

From our EDA and funnel analysis was observed areas for improvement as well as elements that have questions the health of Metrocar as a business.
In the following sections, we will describe our process, findings and conclusion.


### Table of Contents<br>
[1 - Usage]([# 1---Usage])<br>
2 - Project Structure<br>
3 - Data<br>
4 - Analysis<br>
5 - Results<br>
6 - Visualizations<br>
7 - Conclusions<br>
8 - Acknowledgment<br>
9 - Contact<br>


### 1 - Usage
.ipynb: Google Colab: Upload directly via the "File" menu or open from Google Drive
Jupyter Notebook: Install Jupyter, start it via terminal, and open the .ipynb file through the interface

Upload all .csv files from `data` directory within the open Colab project.
If you are using a local IDE, you may want to update the .ipynb file so to link the .csv to their local directory.


### 2 - Project Structure

```
Metrocar Funnel Analysis/
├── data/ # Reference to dataset and used aggregated dataset at various granularity level
|   ├── app_downloads.csv
|   ├── reviews.csv
|   ├── ride_requests.csv
|   ├── signups.csv
|   └── transactions.csv
|
├── notebooks/ # Jupyter notebooks with the analysis/segmentation code
│   └── Metrocar_Funnel.ipynb
│
├── results/ # Output files, results, project report, .ppt presentation
|   ├── Fake Data Pairplot.png
|   ├── Funnel Ride Age Range.png
|   ├── Funnel Ride Hours.png
|   ├── Funnel Ride Months.png
|   ├── Funnel Ride Platform.png
|   ├── Funnel Ride Weekdays.png
|   ├── Funnel Ride.png
|   ├── Funnel User.png
|   ├── Hist time before boarding ride.png
|   ├── Hist Time Before cancelling ride.png
|   ├── Hist time before request and accept.png
|   ├── Line Plot Acceptance, request, cancel by Day.png
|   ├── Line Plot Acceptance, request, cancel by Month.png
|   ├── Metrocar Presentation.pdf
|   └── Pie Sentiment analysis.png
|
└── README.md #  Project documentation
```


### 3 - Data
For security reasons, the database link cannot be shared.
However, we have provided the 5 tables of the database as .csv document, to be found in the `data` directory.

For information, here is the structure of the database's tables and columns:

`app_dowloads`
```
'app_download_key', 
'platform', 
'download_ts'
```

`reviews`
```
'review_id', 
'ride_id', 
'user_id', 
'driver_id', 
'rating',
'review'
```

`ride_requests`
```
'ride_id', 
'user_id', 
'driver_id', 
'request_ts',
'accept_ts', 
'pickup_location', 
'dropoff_location', 
'pickup_ts',
'dropoff_ts', 
'cancel_ts'
```

`signups`
```
'user_id', 
'session_id', 
'signup_ts', 
'age_range'
```

`transactions`
```
'transaction_id', 
'ride_id', 
'purchase_amount_usd',
'charge_status', 
'transaction_ts'
```

### 4 - Analysis
We conducted our analysis in the following:
* EDA
* Wrangle data to generate Funnel per user at various levels:
- user downloaded
- user signup 
- user request
- user acceptance
- user started
- user completed
- user has paid
- user cancelled
- user paid
- user rated
- user review
* Visualizing Funnel per user
* Wrangle data to generate Funnel per ride at various levels:
- ride request
- ride acceptance
- ride completed
- ride paid
- ride rated
* Visualizing funnel per ride by:
- hour
- weekdays
- months
- age range
- platform
* Additional observations related to time spent on the app
* Sentiment analysis on user's reviews

### 5 - Results
* We observed 3 major drop-offs on the funnel per user at Signups, request ride, review levels.
* Largest drop-offs act rider acceptance level for the funnel per ride
* Peak of activity between 8 and 10 a.m. and between 4 and 8 p.m.
* Observed 1/3 of requests are refused, a trend that is observable throughout the day
* Ride are accepted within 10 minutes
* Average of 12 minutes between a request and a cancellation
* iOS users represent our largest demographic with 60% of users, followed by Android, 30%, and Web, 10%
* We have two dominant age groups: 35-44, 25-34
* An unknown age group should be investigated further as it shapes the largest group of 
* Reviews and rating are mild: average 3 out 5 for rating and a 45% of negative opinion expressed about
* We observed a concerning plummeting of Metrocar's activity from December 2021 to latest record on April 2024: Metrocar's activity are close to 0 by April 2024

### 6 -  Visualizations
Charts and plots are available in the following folder: `results`

### 7 - Conclusions

**Funnel at user level**<br>
Looking at the Funnel per user we observed 3 major drop-offs:<br>
*Signups*, *request ride*, *review*

* After investigating these levels, we concluded it difficult to provide thorough advice for each of them due to lack of data.
* 25% of users who downloaded the app failed to signup, additionally successful signups also left some information blank in their profile. This indicates a possible over-complication of the registration process, which may stop users from passing the download phase.
* 22% of users who signed up did not make their first ride request.
We didn’t have access to relevant data at this level; we recommend checking users’ actions within the app.
<br>
<br>

**Funnel at ride level**<br>
On the Funnel per ride, we observe that the largest drop-offs happen during the driver acceptance phase.<br>
This supports our finding on the Funnel per user where the largest drop-off occurs at the same level.
<br>
<br>

**User and ride per day**<br>
Observing activity throughout the day, we notice two peaks during expected rush hours:<br>
* Between 8 and 10 a.m.<br>
* Between 4 and 8 p.m.<br>


From the graphic, we can also see that the number of driver refusals is proportional to the number of ride requests, with approximately one-third of requests being refused by drivers consistently throughout the day.<br>
Despite this pattern, we recommend deploying more drivers during these peak hours to accommodate the high volume of ride requests.<br>
Additionally, if we consider implementing surge pricing, these hours would be the optimal times to do so.
<br>
<br>

**Cancelling policy and fee**<br>
A closer examination of the time users spend requesting, onboarding, or canceling a ride reveals that most rides are accepted within 10 minutes. Additionally, there is an average of 12 minutes between the time a user requests and cancels a ride.<br>
It is likely that we are losing users and business opportunities by allowing users to cancel their rides freely. Therefore, we propose implementing a cancellation fee for users who cancel within the first 10 minutes after requesting a ride. We also recommend offering a replacement solution for users who have been waiting at least 10 minutes after requesting a ride.
<br>
<br>

**Platform**<br>
In our funnel by platform, we see a similar drop-off ratio for every group. <br>
However, the iOS platform is responsible for 60% of our ride requests, android is second with 30%, and finally web for the final 10%. We recommend following the same ratio for the marketing budget.
<br>
<br>

**Age groups**<br>
In the funnel by age range, we can see a large unknown group. However, a majority of users with known age ranges fall between 35-44 and 25-34 which make up 30% and 20% of our user base with available age information. <br>
We hard encourage to focus on these larger groups, as a market campaign might yield more fruitful results proportionally to their sizes.<br>
<br>
The large unknown group should be investigated further.
<br>
<br>

**Reviews**<br>
We ran a sentiment analysis over the reviews which revealed that 45% of the reviews have a negative sentiment and our average rating is 3 out of 5.<br>
We recommend a deeper look into the negative reviews to identify areas of improvement.
<br>
<br>

**Users per month**<br>
Lastly, we saw a constant growth in ride requests, with a proportional lack of acceptance from drivers. The number of cancellations however remained fairly stable.<br>
<br>
However, there is a sharp plummet in 2022. There may be a problem with data collection, structural issues in the app, or, less likely, a sudden drop-off from users. This should be investigated further.


### 8 - Acknowledgment

This project has been conducted within the frame of Masterschool Data Analytics boot camp.
This project was initially conducted as a group composed of Bertrand Flanet, Sidddeq Asmad, and Nadyia Zahn.
However, all the documents, code and visualizations in the directory are of my doing - except for the Metrocar Presentation.pdf which was a collective work.

### 9 - Contact
Bertrand Flanet
E-mail: bertrand.flanet@gmail.com
linkedIn: https://www.linkedin.com/in/bertrand-flanet-67b1b2299/
