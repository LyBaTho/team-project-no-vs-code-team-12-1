# Do influential Yelp users give higher ratings to take-out restaurants compared to non-influential users, and how does the factor of location affect these ratings?

![image](https://miro.medium.com/v2/resize:fit:1012/1*6mGFJh8XrCqOlBRRvf2Deg.png)

## Introduction
Since its launch in 2004, Yelp, as one of the largest online review platforms, has played a crucial role in shaping the reputations of businesses, particularly in the food industry. While there is an abundance of research analyzing Yelp reviews (*Agarwal, Pelullo, & Merchant 2019; Arthur, Etzioni, & Schwartz, 2019*), most studies focus on general patterns of consumer behavior (*Fogel, J. and Zachariah, S., 2017*), sentiment analysis (*Guerreiro & Rita, 2020*), or the detection of fake reviews (*Lee, Ham, Yang, & Koo, 2018*). What these studies largely overlook, however, is the significant role that influential users—those with elite status, numerous followers, or high review counts—play in shaping business ratings (*Pranata, I. and Susilo, W., 2016*). These users wield disproportionate influence on the platform, and their ratings are often perceived as more credible and trustworthy than those of regular users (*Tucker, T., 2011*).

### Research Motivation
In competitive sectors like the food industry, where reputation can make or break a business, understanding the impact of these influential users is essential, as evidenced in a study conducted by  *Nakayama and Wan (2018)* about one-third of customers rely on online reviews when choosing a restaurant and over half of 18-to-34-year-olds factor reviews into their dining decisions. Moreover, while the food industry on Yelp has been extensively studied (*Anderson and Magruder, 2012*) because of its tremendous impacts on business outcomes (*Luca, 2016*), the take-out restaurant niche has received minimal attention. The majority of existing studies on take-out restaurants emphasize negative aspects such as health risks, obesity, and food safety concerns (*Jeffery et al., 2006; Baek et al., 2022*). These studies tend to focus on the health implications of frequent take-out consumption but fail to address the consumer dynamics on platforms like Yelp, where reviews have the power to influence public perception and business success (_Jiménez, et al. 2013_). Additionally, location, particularly in terms of region, state, and city, plays a pivotal role in how take-out restaurants are rated on Yelp (_Tayeen, et al., 2019_). Regional preferences can influence the types of cuisines that receive higher ratings, with some regions showing a stronger preference for local or niche food options (_Rahimi, et al., 2018_). State-level factors such as regulations, food safety laws, and even cultural food trends may also impact how users perceive and rate take-out establishments. Additionally, within cities, neighborhood dynamics like the level of urbanization, socio-economic status, and competition with nearby restaurants can lead to significant variations in ratings (_Tayeen, et al., 2021_). Influential Yelp users in major metropolitan areas may also drive more reviews and higher visibility for restaurants, skewing ratings compared to those in smaller cities or rural areas. This gap in the literature calls for a deeper investigation into how influential users interact with take-out restaurants, especially as take-out has become increasingly important in the post-pandemic dining landscape.

The accessibility and usefulness of the output from this study significantly benefit other students and the larger scientific community. By **developing an automated and reproducible workflow using open-source tools like R**, this research provides a template that others can easily adapt for similar analyses. **The study's findings and the associated code** can be shared on public platforms like GitHub, making them readily available for educational purposes and further research. The workflow includes data extraction, cleaning, transformation, and modeling processes, all documented and scripted to ensure transparency and repeatability. Moreover, the **comprehensive PDF report** serves as a valuable resource that clearly communicates the research methods, analyses, and findings. It can be used as a teaching tool in academic settings, demonstrating how to approach complex data analyses and interpret results within a real-world context.

### Research Question
This study aims to address the gap in the dynamics of online reviews, particularly from influential Yelp users, by asking: **Do influential Yelp users give higher ratings to take-out restaurants compared to non-influential users, and how does the factor of location affect these ratings?** This research is critical for several reasons. First, understanding the behavior of influential users could help businesses better manage their online reputations, particularly in a niche market like take-out dining. Second, examining how location—whether at the regional, state, or city level—impacts ratings can provide valuable insights into consumer preferences. Location-specific factors, such as regional food trends, city demographics, and neighborhood characteristics, may influence how users perceive and rate businesses. For take-out restaurants operating in highly competitive environments, especially those without an established offline presence, this research could offer practical strategies for improving ratings and attracting new customers by understanding how geographic context shapes consumer perceptions.

### Variable Types

| Variable      | Description                                                         | Data Class | Dataset           |
|---------------|:-------------------------------------------------------------------:|-----------:|-------------------|
| business_id   | A unique character string for each individual business              | numeric    | business dataset  |
| name          | The business name                                                   | character  | business dataset  |
| city          | The city name where the business is located                         | character  | business dataset  |
| state         | The state name where the business is located                        | character  | business dataset  |                                   
| stars         | The average star rating rounded to half-stars                       | numeric    | business dataset  |
| review_count  | The number of reviews                                               | numeric    | business dataset  |
| is_open       | Variable that shows with 0 or 1 of the business is closed or open   | numeric    | business dataset  |
| attributes    | Business attributes to values                                       | character  | business dataset  |
| user_id       | An unique character string as user id                               | numeric    | user dataset      |
| review_count  | The number of reviews                                               | numeric    | user dataset      |
| fans          | The number of fans the user has                                     | numeric    | user dataset      |
| elite         | The years the user was 'elite'                                      | numeric    | user dataset      |
| user_id       | An unique character string as user id                               | numeric    | review dataset    |
| business_id   | A unique character string for each individual business              | numeric    | review dataset    |
| review_id     | Unique review id                                                    | numeric    | review dataset    |
| stars         | The average star rating rounded to half-stars                       | numeric    | review dataset    |

### Conceptual Model


## Research Method and Results 
### Data Source
From the Yelp database the business, user, and review data files are downloaded to answer the research question. 
- **Yelp Database:** https://www.yelp.com/dataset/download

Since the file is in .tar format, we need to extract it into separate JSON files by using R. The next step is to convert the JSON files into CSV format using Python code.  You can find the R & Python code here:
- **Extracting JSON files:** [LINK](https://github.com/course-dprep/team-project-no-vs-code-team-12-1/blob/main/4-testing_code/tar_format_to_json_converter.R)
- **Converting CSV files:** [LINK](https://github.com/course-dprep/team-project-no-vs-code-team-12-1/blob/main/5-external_code/json_to_csv_converter.py)

Finally, run the script from your terminal with the following command and replace *yelp_academic_dataset.json* with the path to the JSON file you wish to convert. The script will generate a CSV file with the same name as your input JSON file, located in the same directory.

```{r}
python json_to_csv_converter.py yelp_academic_dataset.json
```

To streamline the process, we've provided an R script that **automatically downloads all the necessary data sets for this study only**. Simply copy and run the code, and it will retrieve all required files directly into your working directory. However, please be aware that for the code to function properly, you’ll need to install both the **googledrive** and **tidyverse** packages. These packages are crucial, especially when dealing with large files, as they ensure smooth data handling and integration within your R environment.
- **Link R script:** [LINK](https://github.com/course-dprep/team-project-no-vs-code-team-12-1/blob/main/6-source_code/download_data.R) 

**Note:** Due to **limitations such as computational memory constraints and the focus on a manageable dataset for in-depth analysis**, we have decided to analyze a **reduced sample of 32,576 observations from the Yelp dataset**. This sample size allows us to perform comprehensive statistical analyses while maintaining computational efficiency. **Future research can extend this work by examining the entire population of Yelp reviews**, which could validate our findings on a larger scale and potentially reveal additional insights into the behavior of influential users in the context of take-out restaurants.

### Research Method
To explore these relationships, **regression analysis** will be employed as the primary research method. This method is well-suited for controlling multiple factors such as restaurant location, business attributes (e.g., parking, takeout options), and user metrics (e.g., yelping_since, fans, elite status). By using regression, we can isolate the effect of user influence on ratings and better understand the causal relationships at play. The analysis will focus on key variables like user profiles (including elite status, review count, and average stars), and business characteristics from the Yelp dataset. This approach will help to provide a clearer picture of how influential users impact the ratings of take-out restaurants compared to non-influential users.

### Result  
#### Exploratory Analysis
**Distribution of User Ratings by Elite Review Status**
To understand how user ratings vary between elite and non-elite reviewers, we analyzed the distribution of stars_user across both groups. As shown in Figure 1 ("distribution_user_ratings_by_elite_review.png"), elite reviewers tend to give slightly higher ratings compared to non-elite reviewers. Specifically, around 3000 of elite reviews are 5-star ratings, whereas over 12,000 of non-elite reviews achieve the same. This suggests that non-elite users may have a more positive perception or are more generous in their evaluations.
![Figure 1](https://github.com/course-dprep/team-project-no-vs-code-team-12-1/blob/main/7-plots/distribution_user_ratings_by_elite_review.png)

**Average User Rating by Region and Elite Review Status**
Geographic location can influence consumer preferences and ratings. We calculated the average user rating (avg_rating) for each region, segmented by elite_review status. Figure 2 ("user_ratings_by_region_elite_review.png") illustrates that in regions like the Pacific and New England, elite reviewers provide higher average ratings (4.5 stars) compared to non-elite reviewers (4.0 stars). Conversely, in the Midwest, both elite and non-elite reviewers give similar average ratings (4.2 stars), indicating regional differences in rating behaviors.
![Figure 2](https://github.com/course-dprep/team-project-no-vs-code-team-12-1/blob/main/7-plots/user_ratings_by_region_elite_review.png)

**Impact of Business Open Status and Review Counts**
We examined the review_count_business to see how it varies between open and closed businesses. Figure 3 ("distribution_review_count_business_by_is_open.png") shows that open businesses generally have higher review counts, with a peak of around 500 reviews, while closed businesses peak at around 200 reviews. This could imply that higher engagement correlates with business longevity.
![Figure 3](https://github.com/course-dprep/team-project-no-vs-code-team-12-1/blob/main/7-plots/distribution_review_count_business_by_is_open.png)

To explore whether the volume of reviews affects user ratings, we analyzed businesses with more than 1,000 reviews and those with fewer than 1,000 reviews.
**High Review Counts (>1000):**
Figure 4 ("avg_rating_gt_1000_by_region.png") reveals that for businesses with high review counts, elite reviewers consistently give higher average ratings across all regions. For example, in the South Atlantic region, elite reviewers give an average rating of 4.7 stars, while non-elite reviewers give 4.3 stars.
![Figure 4](https://github.com/course-dprep/team-project-no-vs-code-team-12-1/blob/main/7-plots/avg_rating_gt_1000_by_region.png)

Figure 5 ("avg_rating_gt_1000_by_is_open.png") indicates that open businesses receive higher average ratings from both elite (4.6 stars) and non-elite (4.4 stars) reviewers compared to closed businesses.
![Figure 5](https://github.com/course-dprep/team-project-no-vs-code-team-12-1/blob/main/7-plots/avg_rating_gt_1000_by_is_open.png)

**Low Review Counts (<1000):**
Figure 6 ("avg_rating_lt_1000_by_region.png") shows a smaller gap between elite and non-elite reviewers. In some regions, non-elite reviewers even give slightly higher ratings.
![Figure 6](https://github.com/course-dprep/team-project-no-vs-code-team-12-1/blob/main/7-plots/avg_rating_lt_1000_by_region.png)

Figure 7 ("avg_rating_lt_1000_by_is_open.png") suggests that for businesses with low review counts, the difference in average ratings between open and closed businesses is minimal, regardless of elite status.
![Figure 7](https://github.com/course-dprep/team-project-no-vs-code-team-12-1/blob/main/7-plots/avg_rating_lt_1000_by_is_open.png)

These findings imply that elite reviewers tend to rate highly popular businesses more favorably, possibly due to better experiences or higher expectations met.

**Average Rating by Elite Status**
Focusing on take-out restaurants (take_out == 1), we assessed whether elite reviewers rate them differently. Figure 8 ("avg_rating_takeout_by_elite_review.png") shows that elite reviewers give an average rating of 4.5 stars, while non-elite reviewers give 4.2 stars. This indicates a positive bias from elite reviewers towards take-out establishments.
![Figure 8](https://github.com/course-dprep/team-project-no-vs-code-team-12-1/blob/main/7-plots/distribution_ratings_takeout_by_elite_review.png)

**Distribution of User Ratings by Region and Elite Status**
To delve deeper, we examined the distribution of user ratings for take-out restaurants across regions.

Figure 9 ("distribution_ratings_takeout_by_region_and_elite_review.png") presents boxplots of stars_user by region and elite_review. In regions like the Mountain and Pacific, elite reviewers exhibit higher median ratings and less variability, suggesting consistent positive experiences.
![Figure 9](https://github.com/course-dprep/team-project-no-vs-code-team-12-1/blob/main/7-plots/distribution_ratings_takeout_by_region_and_elite_review.png)

Figure 10 ("distribution_ratings_takeout_by_elite_review.png") consolidates this information, showing that elite reviewers generally provide higher ratings with fewer low-rating outliers compared to non-elite reviewers.
![Figure 10](https://github.com/course-dprep/team-project-no-vs-code-team-12-1/blob/main/7-plots/distribution_ratings_takeout_by_elite_review.png)

These observations reinforce the notion that elite reviewers perceive take-out restaurants more favorably, possibly due to selective dining choices or differing expectations.

**Correlation Analysis**
We computed the correlation matrix for numerical variables to identify potential relationships. Figure 11 ("correlation_matrix_heatmap.png") displays the heatmap of correlations.
![Figure 11](https://github.com/course-dprep/team-project-no-vs-code-team-12-1/blob/main/7-plots/correlation_matrix_heatmap.png)

**Relationship Between Number of Fans and User Rating**
We explored whether a user's popularity (fans) affects their ratings (stars_user), considering the business's open status and region.

Figure 12 ("relationship_fans_user_rating_faceted_by_region.png") presents scatterplots of fans vs. stars_user, colored by is_open and faceted by region. The red regression lines indicate the trend within each region.
![Figure 12](https://github.com/course-dprep/team-project-no-vs-code-team-12-1/blob/main/7-plots/relationship_fans_user_rating_faceted_by_region.png)

Observations include:

- In most regions, there is a slight positive trend, suggesting that users with more fans tend to give marginally higher ratings.
- The trend is more pronounced in regions like the Pacific and Middle Atlantic, where users with more fans give significantly higher ratings to open businesses.
- Closed businesses do not exhibit a clear trend, possibly due to fewer data points or varying reasons for closure.

#### Statistical Analysis


## Relevance of Analysis / Future Applications
The analysis conducted in this study holds significant relevance for a diverse range of stakeholders, including take-out restaurant owners, online review platforms, consumers, and the academic community. By shedding light on the influence of elite Yelp users and the impact of location on restaurant ratings, the research addresses critical gaps in the current understanding of online consumer behavior within the niche of take-out dining.

- **For Business Owners and Marketers:** Understanding that influential Yelp users wield disproportionate power over restaurant ratings enables take-out businesses to strategize more effectively. Restaurants can prioritize engaging with these users through exceptional service, personalized experiences, or targeted marketing campaigns. By recognizing the nuances of how location affects ratings, businesses can tailor their offerings to meet regional preferences and cultural tastes. This is especially pertinent in the post-pandemic era, where take-out services have surged, and competition is fierce. Insights from this study could inform menu development, promotional strategies, and customer engagement practices that resonate with local consumers and influential reviewers alike.
- **For Online Review Platforms:** Platforms like Yelp could utilize the findings to refine their algorithms and user interface designs. By understanding the outsized impact of elite users, platforms might consider weighting systems that balance reviews more equitably or highlight a diversity of opinions. Additionally, recognizing location-based disparities in ratings could lead to the development of more localized review aggregation, helping users find the most relevant and accurate information based on their geographic context.
- **For the Academic and Scientific Community:** The research contributes to the broader literature on online reviews, influencer impact, and consumer behavior in digital marketplaces. By focusing on a previously underexplored niche—take-out restaurants—and incorporating the variable of location, the study opens new avenues for scholarly inquiry. Future research can build upon the methodology and findings to explore other sectors or delve deeper into regional cultural influences on consumer behavior.
- **Future Applications:** Given the increasing reliance on online platforms for consumer decision-making, the implications of this study are far-reaching. Businesses can develop strategies to engage with influential users proactively, potentially improving their ratings and attracting new customers. Online platforms might implement features that promote a more balanced representation of user opinions. Academics can use the study as a springboard for further exploration into the dynamics of online influence and regional consumer preferences.

## Repository Overview
This repository contains a structured workflow for downloading, preparing, preprocessing, and analyzing data to find insights about take-out restaurant ratings. The process is automated using a Makefile, ensuring each step runs in sequence.

### Repository Structure
```plaintext
├── README.md
├── makefile
├── updated-project
├── .Rhistory
├── .RData
├── .gitignore
├── 1-docs
│   ├── Group Report
├── 2-temporary_data
│   ├── cleaned_sample_data
│   ├── sample_data_elite_encoder
│   ├── business_data.csv
│   ├── user_data.csv
│   ├── review_data.csv
│   ├── sample_data.csv
├── 3-final_data
│   ├── takeout_data.csv
├── 4-testing_code
│   ├── download_files_automatically.R
│   ├── label_elite_users.R
│   ├── matching_elite_format.R
│   ├── tar_format_to_json_converter.R
├── 5-external_code
│   ├── json_to_csv_converter.py
├── 6-source_code
│   ├── 0_install_packages.R
│   ├── 1_download_data.R
│   ├── 2_prepare_data.R
│   ├── 3_preprocessing_data.R
│   ├── 4_plot_data.R
│   ├── 5_analyse_data.R
├── 7-plots
```

## Dependencies
Please follow the installation guides at [LINK](http://tilburgsciencehub.com/)
- **Python**: [Installation guide](https://tilburgsciencehub.com/topics/computer-setup/software-installation/python/python/)
- **R**: [Installation guide](https://tilburgsciencehub.com/topics/computer-setup/software-installation/rstudio/r/)
- **Make**: [Installation guide](https://tilburgsciencehub.com/topics/automation/automation-tools/makefiles/make/)
- **GitBash**: [Installation guide](https://git-scm.com/downloads)

To knit RMarkdown documents, make sure you have installed the ```reticulate``` package in R to render Python code

For Python, make sure you have installed the following packages:
```{}
pip install argparse
pip install csv
pip install json
pip install os
```

For R, make sure you have installed the following packages:
```{}
install.packages("tidyverse")
install.packages("here")
install.packages("googledrive")
install.packages("reticulate")
```

## Running Instructions
To execute this study, the source code will be run in the correct sequence, ultimately producing the analysis results. You can run the ```Makefile``` by following these steps:

1. **Clone the Repository:**
   - Fork this repository and you will have the link ```https://github.com/{your username}/team-project-no-vs-code-team-12-1```
   - Open GitBash in your preferred file location
   - Type
```
git clone https://github.com/{your username}/team-project-no-vs-code-team-12-1
```
2. **Set the Working Directory:**
   - Type
```
cd team-project-no-vs-code-team-12-1
```
3. **Run the Workflow:**
   - Open the Command Prompt (terminal) in the working directory
   - Type
```
make
```
   - Wait approximately 40 - 50 minutes for the entire project to run
4. **Clean Temporary and Final Data:**
   - Type
```
make clean
```

**Note:** If you want to run each source code separately, this should be done in the following order:

1. 0_install_packages.R
2. 1_download_data.R
3. 2_prepare_data.R
4. 3_preprocessing_data.R
5. 4_plot_data.R
6. 5_analyse_data.R

**Run the source code separately:**
   - Open the Command Prompt (terminal) in the working directory
   - Type
```
Rscript <file_name.R>
```

## Contributors
This repository was created for the Data Preparation and Workflow Management course, taught by **Hannes Datta** at the Tilburg School of Economics and Management, as part of the Master's program in Marketing Analytics. It is a collaboration by Team 12, consisting of:
- Kris Bruurs - k.bruurs@tilburguniversity.edu 
- Ly Ba Tho - b.t.ly@tilburguniversity.edu
- Jelle de Bie - j.debie@tilburguniversity.edu
- Zeynep Yavlal - z.yavlal@tilburguniversity.edu
- Bart van de Mortel - b.h.l.vdmortel@tilburguniversity.edu

## Research Reference
- Agarwal, A.K., Pelullo, A.P. and Merchant, R.M., 2019. “Told”: the word most correlated to negative online hospital reviews. Journal of General Internal Medicine, 34, pp.1079-1080.
- Anderson, M. and Magruder, J., 2012. Learning from the crowd: Regression discontinuity estimates of the effects of an online review database. The Economic Journal, 122(563), pp.957-989.
- Arthur, J.R., Etzioni, D. and Schwartz, A.J., 2019. Characterizing extremely negative reviews of total joint arthroplasty practices and surgeons on Yelp. Arthroplasty Today, 5(2), pp.216-220.
- Baek, S., Suk, Y., Lee, H. and Ham, S., 2022. The influence of customer perception about food safety on the use of restaurant food delivery or takeout. Journal of the Korean Dietetic Association, 28(3), pp.182-194.
- Fogel, J. and Zachariah, S., 2017. Intentions to use the Yelp review website and purchase behavior after reading reviews. Journal of Theoretical and Applied Electronic Commerce Research, 12(1), pp.53-67.
- Guerreiro, J. and Rita, P., 2020. How to predict explicit recommendations in online reviews using text mining and sentiment analysis. Journal of Hospitality and Tourism Management, 43, pp.269-272.
- Jeffery, R.W., Baxter, J., McGuire, M. and Linde, J., 2006. Are fast food restaurants an environmental risk factor for obesity? International Journal of Behavioral Nutrition and Physical Activity, 3, pp.1-6.
- Jiménez, F.R. and Mendoza, N.A., 2013. Too popular to ignore: The influence of online reviews on purchase intentions of search and experience products. Journal of Interactive Marketing, 27(3), pp.226-235.
- Lee, K., Ham, J., Yang, S.B. and Koo, C., 2018. Can you identify fake or authentic reviews? A fsQCA approach. In Information and Communication Technologies in Tourism 2018: Proceedings of the International
- Conference in Jönköping, Sweden, January 24-26, 2018 (pp. 214-227). Springer International Publishing.
- Luca, M., 2016. Reviews, reputation, and revenue: The case of Yelp.com. Com (March 15, 2016). Harvard Business School NOM Unit Working Paper, (12-016).
- Nakayama, M. and Wan, Y., 2019. The cultural impact on social commerce: A sentiment analysis on Yelp ethnic restaurant reviews. Information & Management, 56(2), pp.271-279.=
- Pranata, I. and Susilo, W., 2016. Are the most popular users always trustworthy? The case of Yelp. Electronic Commerce Research and Applications, 20, pp.30-41.
- Rahimi, S., Mottahedi, S. and Liu, X., 2018. The geography of taste: using Yelp to study urban culture. ISPRS International Journal of Geo-Information, 7(9), p.376.
- Tayeen, A.S.M., Mtibaa, A., Misra, S. and Biswal, M., 2021. Impact of Locational Factors on Business Ratings/Reviews: A Yelp and TripAdvisor Study. Big Data and Social Media Analytics: Trending Applications, pp.25-49.
- Tayeen, A.S.M., Mtibaa, A. and Misra, S., 2019, August. Location, location, location! quantifying the true impact of location on business reviews using a Yelp dataset. In Proceedings of the 2019 IEEE/ACM
- International Conference on Advances in Social Networks Analysis and Mining (pp. 1081-1088).
- Tucker, T., 2011. Online word of mouth: characteristics of Yelp.com reviews. Elon Journal of Undergraduate Research in Communications, 2(1), pp.37-42.
