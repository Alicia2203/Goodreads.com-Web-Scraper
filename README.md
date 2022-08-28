# Goodreads.com-Web-Scraper

## Introduction

The web page that we have chosen to scrape from is a page that displays a list of  “Best Books Ever” from goodreads.com. Goodreads is an American social cataloging website and a subsidiary of Amazon that allows individuals to search its database of books, annotations, quotes, and reviews. As books lovers, our group decided that it would be interesting for us to find interesting insights from the top 100 “Best Books Ever” that was voted on by the general Goodreads community. Although there are existing web scraping solutions on the internet, they are mostly more complicated as they usually involve scraping all the books (around 10000 books) from the goodreads webpage. For this assignment, we think it would be appropriate for us to only scrape 100 books using R, hence our script differs from the other solutions found online. However, we did use one of the solutions online as a reference while building the structure of our program. What differs our solution from theirs is that we scraped different variables, we scraped a different webpage, and we scraped a much smaller scale of the data. The data that we have scraped from our chosen web page are the Rank, Goodreads ID, Book Title, Author, Average Rating, Number of Ratings, Score, Number of Voters, Most Voted Genre, and Awards (whether or not the book has received any). For this project, we will be focusing on finding what kind of books are more likely to be liked by readers.

**Goodreads Web Page URL:** https://www.goodreads.com/list/show/1.Best_Books_Ever?page=1

## Descriptive Analysis

![image](https://user-images.githubusercontent.com/69787181/187073469-35a9bf9d-7506-4100-bf90-dba3fd36401c.png)
The histogram above was generated and displayed to observe the Average Ratings among the top 100 books that readers would give to the books. Histogram is very useful for comparing distributions as it provides visual interpretations. According to this histogram (Diagram 1), it illustrates symmetrical distributions and almost a normal distribution graph but tends towards a random distribution at the higher ratings. It shows a continuous variable of ratings in the horizontal axis (x-axis), whereas the vertical axis (y-axis) illustrates the number of readers. Moreover, the height of the bar demonstrates the count of readers given to the ratings. The histogram illustrates that the majority of readers gave around a 4.3 rating on average for the books.

![image](https://user-images.githubusercontent.com/69787181/187073480-aac58851-4c6f-4f70-8d3f-c61bae83c34f.png)

Diagram 2 illustrates a boxplot of the average ratings for the Top 100 books scrapped. According to the histogram above (Diagram 2), the length of the left and right tail of the boxplot are equal. Therefore, we can conclude that the data is normally distributed. The minimum rating of the books are 3.98, and maximum are 4.28. Besides that, the boxplot shows that the median of rating is around 4.12, and the data shows little to no skew, which means that the distribution of the data is symmetrical. In conclusion, we can conclude that the majority of readers of the top 100 books gave a good rating for the books.

![image](https://user-images.githubusercontent.com/69787181/187073490-f357a4d3-524f-46d7-b1fb-89a7d4154d24.png)

Diagram 3 displays the histogram of the scores given by readers to the books. As observed from the histogram above, the data are left skewed and most of the data values are clustered on the left side of the histogram. It can be observed that the majority of readers gave around 500000 scores for the books that they have read. The book's total score is based on multiple factors, including the number of readers who have voted and how highly those voters ranked the book. The sample data size collected for this histogram is 100 books, thus, we believe that each bar on the histogram contains enough data points to accurately show the distribution of the data. However, we have identified a few outliers at the score around 2500000. Thus, this means that there are not many books that have received such a high score. 

![image](https://user-images.githubusercontent.com/69787181/187073499-0e426af0-64a7-4cc9-8b59-c6498bfa67a5.png)

Diagram 4 above shows comparing two sets of boxplots, one for the books awarded (right) and one for the books not awarded (left). We created the boxplot to observe the relationship between the awarded books and not awarded books against the average rating of the top 100 books to identify if there’s any pattern between these 2 variables. From the boxplot of the not awarded books (left), we can identify that the boxplot is a symmetric distribution, which means that the data scrapped are normally distributed. Moreover, the whiskers are about the same length on both sides of the box, thus, we can conclude that the not awarded books have the average ratings of the data set that divides the box into two parts as they have the same quarter. However, by looking at the boxplot of books that have received awards, it illustrates a right-skewed boxplot as the median is closer to the lower or bottom quartile, meaning that the data used may not be normally distributed. The lower quartile of the boxplot indicates that 25% of awarded books are below 3.99 ratings, while the upper quartile shows that 75% of awarded books are above 4.3 ratings. A wider distribution of whiskers means that it has more scattered data compared to the not awarded books. To conclude, there is no significant relationship between the awards and the ratings.

![image](https://user-images.githubusercontent.com/69787181/187073514-cc53b44d-5b85-4f35-80f8-c0ba03306685.png)

Diagram 5 displays the relationship between 2 sets of data,  which is scores against average ratings of the top 100 books. This scatterplot was generated to observe whether there is a correlation between the score and the average ratings of the books. In this scatterplot, it is observed that most points lie towards the left side of the plot, thus, no correlation is identified. The strength of the scatterplot is moderate, as the distance of the points are only moderately close to each other.  In conclusion, there’s no significant relationship between the average rating and the score.![image](https://user-images.githubusercontent.com/69787181/187073518-c91533b1-4f79-4121-8e32-c9b74daf7b99.png)

![image](https://user-images.githubusercontent.com/69787181/187073533-11fc6881-588a-4042-9fda-e5e9c3ce40a7.png)
Diagram 6 displays the bar chart of most voted genres. This chart is generated to observe the popularity of genres among the top 100 books. From this bar chart, it is observed that the Classics genre has the most counts (40 books) among the other most voted genres in the top 100 best ever books list. This means that although the classics genre is underrepresented on goodreads.com, it is highly represented in the Top 100 best ever books list, this suggests that readers are more likely to upvote the classics. However, the least popular genres from the top 100 books are Horror, Non-fiction, Novels, and Romance, these genres are least popular among readers.

![image](https://user-images.githubusercontent.com/69787181/187073545-919a6938-28ff-4e5e-8ca3-f39b3182214d.png)

Diagram 7 displays the boxplots of the most voted genres against the average rating of the top 100 books. This boxplot is created to observe the relationship between most voted genres and their average rating on goodreads.com. The results above show that the mean average rating of the fantasy genre is considerably higher than the rest. In contrast, the classics have a larger range of ratings, ranging around 3.9 to 4.2. We can also see that this boxplot gives a compact, quickly assimilated summary of the data, suggesting that differences between genres do not typically have different average ratings. Furthermore, we have identified that there are 2 outliers in the Young adult genre which indicates that some young adult books have an extraordinarily high rating whereas some have an extraordinarily low rating. According to the boxplots in Diagram 7, the genre of Horror, Non Friction, Novels, and Romance has only 1 line without the box. R graphics package will plot a line without a box if lacking of data for that genre.

![image](https://user-images.githubusercontent.com/69787181/187073566-7fd49705-0c6c-455d-9fdc-0a21edea0bd8.png)

We decided to see which genres were more likely to be ranked higher within this top 100 best books ever list. Note: in this scenario, the lower the rank number of the books, the higher the position of the books among the top 100 books. Diagram 8 displays the box plots of the most voted genre against their ranks. It is observed that the boxplot for the Fantasy genre is comparatively the longest, which implies that fantasy books can be ranked high as well as low. The young adult genre has a comparatively shorter box yet still has a higher rank as compared to other genres. Therefore, this suggests that books that are in the young adult category are more likely to be ranked higher. Meanwhile, Horror, Non-fiction, Novels, and Romance seem to be ranked lower in general, because from Diagram 6, it is shown that they are the least popular genres among the listed top 100 books. Additionally, it is observed that there is an outlier in the children’s genre, which indicates that some children's books have extraordinarily high ranks. In conclusion, the boxplots from Diagram 8 illustrate an overall view and performance of different genres of books.

## Conclusion

Based on our findings, our analysis suggested that the majority of readers of the top 100 books gave a good rating for the books and there is no significant relationship between the awards and the ratings as well as the average rating and the score. In addition, our analysis also suggested that fantasy and young adult genres are comparatively more popular whereas horror, non-fiction, novels and romance are comparatively least popular in the top 100 best books. Besides, we also found out that readers are more likely to upvote the classics as there consist of 40 classic books in the top 100 best ever books list.

One biggest limitation of this project is that we were unable to properly scrape all the data from each book’s page due to error in open connection, therefore, there will always be several different missing data for the most voted genre variable in our data set everytime we scrape the web page, this affected the accuracy of our analysis. Besides, the quality of the entire list is also questionable since anyone on the internet can vote, hence we decided to scrape the top 100 books as we believe that the higher the book is ranked, the more accurate the data is in giving us insight of which and what types of books are more likely to be liked by readers. Moreover, 100 books is still a relatively small amount of data as categorised into different genre; therefore, there’s a high possibility that our data is biased. 













