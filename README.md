# WebScraping-and-RegularExpression
library(rvest)
#Case1 for scraping
films <- read_html("https://en.wikipedia.org/wiki/List_of_highest-grossing_films") %>% 
  html_table(fill = TRUE)

# extract all the table
films

#get only the first number
films <- films %>% 
  `[[`(1)
films

# replace something we don't want
gsub(",|\\$", "", films$`Worldwide gross`)


# replace F in row 19
# what ahead a dollar sign (look ahead) : replace it as ""
gsub(".*(?=\\$)|", "", films$`Worldwide gross`, perl = TRUE)



# Case2 for scraping
jokerHTML <- read_html("https://www.rottentomatoes.com/m/joker_2019") 
# get the whole html in the id node
jokerHTML %>% 
  html_nodes("#movieSynopsis")

# get the text in the tab
jokerHTML %>% 
  html_nodes("#movieSynopsis")%>%
  html_text()

# get the tomatometer %
jokerHTML %>% 
  html_nodes(".mop-ratings-wrap__percentage") %>% 
  html_text()
