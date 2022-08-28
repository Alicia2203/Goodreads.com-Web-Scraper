# THIS PROGRAM SCRAPES THE TOP 100 BOOKS FROM THE BEST BOOKS EVER LISTS FROM GOODREADS.COM

library(rvest)
library(dplyr)
library(scales)
library(magrittr)
library(ggplot2)
library(tidyverse)

# Function that scrapes the most voted genre type of each book
get_genre<-function(booklink){
  genre<-booklink %>% 
         html_nodes('.elementList:nth-child(1) .left .bookPageGenreLink')
  
  if(length(genre)==0){
    genreVoted=NA
  }
  else{
    genreVoted<-gsub( " *<.*?> *", "", genre)
  }
  return(genreVoted)
}

# Function that returns whether or not a book has received awards
get_award <-function(booklink){
  award<- booklink %>% 
                  html_nodes('.clear+ .clearFloats .infoBoxRowItem')
  if(length(award)==0){
    hasAward<-FALSE
  }
  else{
    hasAward<-TRUE
  }
  return(hasAward)
}

# The main webscraping function
goodReads_webscrape<-function(listUrl){
  
  # This function takes the url of the main book list page, scrapes it, and collects urls of each book's page, 
  # goodReads ID's, titles, authors, rating, number of ratings, score and number of voters.
 
    data = data.frame()

    list_page = read_html(listUrl)
    
    rank = 1:100
    
    # Scrape the title of the books
    title = list_page %>% 
                      html_nodes(".bookTitle span") %>% 
                      html_text()
    
    # Scrape the author of the books
    author = list_page %>% 
                      html_nodes(".authorName span") %>% 
                      html_text()
    
    # Scrape the ratings of the books
    rating = list_page %>% 
                      html_nodes(".minirating") %>% 
                      html_text() %>% 
                      str_extract("\\d+\\.*\\d*") %>%
                      as.numeric()
    
    # Scrape total number of rating for each book
    no_ratings = list_page %>% 
                          html_nodes(".minirating") %>% 
                          html_text() %>% 
                          strsplit(" — ") %>%
                          sapply("[[",2) %>%
                          strsplit(" ") %>%
                          sapply("[[",1) %>% 
                          gsub(",", "", .)  %>% 
                          as.numeric()
    
    # Scrape the score of the books
    score = list_page %>%
                        html_nodes (".uitext a:nth-child(1)") %>%
                        html_text() %>%
                        strsplit(" ") %>%
                        sapply("[[",2) %>%
                        gsub(",", "", .)  %>%
                        as.numeric()
                    
    # Scrape the number of votes for each book  
    pplvoted = list_page %>% 
                          html_nodes(".uitext .greyText+ a") %>% 
                          html_text()%>%
                          strsplit(" ") %>%
                          sapply("[[",1) %>%
                          gsub(",", "", .)  %>% 
                          as.numeric()
    
    # Scrape part of the url of the book page
    book_hyper = list_page %>% 
      html_nodes("div.leftContainer")%>%
      html_nodes("td")%>%
      html_nodes('a.bookTitle')%>%
      html_attr("href")
    
    # Extract Goodreads book ID from url, which can be used as a key variable. Second gsub() is used to catch an occasional exception
    goodreadsID = gsub(".*/book/show/\\s*|-.*", "", book_hyper)
    goodreadsID = gsub("\\..*","",goodreadsID) %>% as.numeric()
    
    # Combine columns to a dataframe 
    data = cbind(Rank = rank, GoodreadsID = goodreadsID, Book_Title = title, 
                  Author = author, Average_Rating = rating, 
                  Number_of_Ratings = no_ratings, Score = score, 
                  Number_of_Voters = pplvoted)
    
    # To display the progress of the running program
    cat("\n", "Books Found in this list: ", nrow(data),"\n")
  
    # Scrape the page of individual books in the list to get book description, genre and awards

    badurls = 0 # To take note of the number of bad urls
    
    # To assign column data as NA if no data is be assigned later
    book_description = rep(NA,nrow(data)) 
    genreVoted = rep(NA,nrow(data))
    hasAward = rep(NA,nrow(data))
  
    for(i in 1:nrow(data)){
      # The url of each book's page
      url<-paste('https://www.goodreads.com',book_hyper[i],sep='')
      go<-tryCatch(read_html(url),
                   error=function(c) 'stop')
      
      if(go!='stop'){

        booklink <- read_html(url)
      
        #Get additional information for each book
        
        hasAward[i] =  get_award (booklink)
        
        genreVoted[i] =  get_genre (booklink)
        
        }
        else{
          badurls=badurls+1
        }
      
    # To display the progress of the running program
     cat(paste('\n', i, "  ", title[i], sep=''),'\n')
    }
    
    # combine columns to new data frame
     newData = cbind.data.frame(Most_Voted_Genre = genreVoted,
                                 Has_Award = hasAward)
  
    # Combine newly generated data frame with the previous data frame
     Complete_df = cbind(data,newData)
  
  return(Complete_df)}

# call the webscraper function to scrape the website with it's url as the argumenet
BestBooksEver100 = goodReads_webscrape('https://www.goodreads.com/list/show/1.Best_Books_Ever')

# Export dataframe as csv file
write.csv(BestBooksEver100, "BestBooksEver100.csv")

# Inspect the structure of the data frame
str(BestBooksEver100)

################################# PART C ####################################

# Histogram for Average Ratings
ggplot(data = BestBooksEver100, aes(rating))+
  geom_histogram(bins = 25,fill="dodgerblue4")+
  labs(title="Histogram for Average Ratings")+
  labs(x="Average Rating",y="Counts")

# Boxplot for Average Ratings
ggplot(data = BestBooksEver100, aes(y=rating,x=""))+
      geom_boxplot(fill="dodgerblue4",width=0.1)+
      labs(title="Boxplot for Average Ratings")+
      labs(y="Average Rating",x="")

# Histogram for Score
hist(score, breaks = 25)

# Box plot of Has_Award vs Average Rating
qplot(Has_Award, rating, data = BestBooksEver100, 
      geom = "boxplot", fill = Has_Award ) +
  labs(title="Box Plot of Has_Award vs Average Rating")+
  labs(y="Average Rating", x="Has_Award")

# Sctterplot of score vs rating
ggplot(BestBooksEver100, aes(x = score, y = rating)) +
      geom_point() +
      labs(title="Scatterplot of score vs rating")+
      labs(y="Average Rating",x="Score") 

# Bar Chart of Most_Voted_Genre
ggplot(BestBooksEver100, aes(Most_Voted_Genre)) + 
       geom_bar(fill = "steelblue", color ="steelblue") +
       theme_minimal()+
       labs(title="Bar Chart of Most_Voted_Genre")+
       labs(y="Count", x="Most_Voted_Genre")  +
       theme(axis.text.x = element_text(angle = 45)) 

 # Box plot of Most_Voted_Genre vs Average Rating
qplot(Most_Voted_Genre, rating, data = BestBooksEver100, 
       geom = "boxplot", fill = Most_Voted_Genre )  +
       labs(title="Box Plot of Most_Voted_Genre vs Average Rating")+
       labs(y="Average Rating", x="Score")+
       theme(axis.text.x = element_text(angle = 45))

# Box plot of Most_Voted_Genre vs rank 
qplot(Most_Voted_Genre, Rank, data = BestBooksEver100, 
      geom = "boxplot", fill = Most_Voted_Genre )  +
  labs(title="Box Plot of Most_Voted_Genre vs Rank")+
  labs(y="Rank", x="Score")+
  theme(axis.text.x = element_text(angle = 45)) +
  scale_y_reverse()
