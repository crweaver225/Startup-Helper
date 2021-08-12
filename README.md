# Startup-Helper

The majority of businesses fail within the first couple of years of opening. Considering the amount of money, effort, and time involved in starting a business; entrepreuners needs every advantage they can get. This data science project is designed to help entrepreuners figure out where in the city of Chicago they would be most successful in starting their business.

The project will take the restaurant type an entrepreuner is interested in opening and suggest which of Chicago's 77 neighborhoods would be most promising for choosing as the location for their restaurant. Specifically we will be looking at cafe's. The idea behind this project is to see if there is a correlation between a resturant type, population information for different neighborhoods, and likes specific restaurants of that type recieve on Foursquare. The idea behind this is that restaurants who receive higher ratings on Foursquare will receive more patrons. I make the assumption that there might be a correlation between neighborhoods and which types of restaurants are enjoyed.

Steps to achieve

First i will do some web scraping to find dataf for each of Chicago's 77 neighborhoods. Data will include name, population, size in square miles, and demographic breakdown. I will be using BeautifulSoup and will start with web scaping this page: https://en.wikipedia.org/wiki/Community_areas_in_Chicago. I found a csv with further breakdowns of demographics which I will merge with my web crawling data.

I next will need to use the Foursquare api to get data about specific cafe's that are in each of the 77 neighborhoods. I will use the venues/search api and parse data for name, id, and category. I will be sure to track which neighborhood each restaurant is in for training of my model.

I next will use Foursquare to find ratings for each of the cafe's found in step three has recieved. I will use the venues/{venue id} api for this task. Because it looks like I will have over 5k of venues, and because i must make this call for each unique venue, i will have to break this call down to occur over a couple of hours so that I dont go over my Foursquare api call limit.

Once all this data is collected, i next need to do some data wrangling. This involves doing one hot encoding on all the restaurant types for each record and normalizing the rest of the data (population information). I first considered also one hot encoding the neighborhood name as well, but I am already looking at over 100 dimensions with the restaurant type and am very skeptical thats not too much. So the rest of the demographic and size data for each neighborhood will suffice as it is unique per neighborhood.

I will next build a model that can take in examples of data (restaurant type, neighboorhood information) and accurately predict the rating that venue recieved. If the model works well, we can take any resturant type, and see which neighboorhood it would receive the most likes in. This provides an entrepreuner good information on where they might be most successful. I will be attempting a linear regression model as I need a continous output for an estimate of likes.

I am skeptical that I will be able to build a model using the large number of dimensions in step 5. So as a backup, I will further data wrangle to only grab records for a specific restaurant type and therefore not need to feed one hot encoded data to signify each venue type. This would mean I will need a different model for each restaurant type, but this will probably be more appropriate for a simple Linear model anyways.
