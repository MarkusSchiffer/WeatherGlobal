For my final project, I would like to create a website, CarGuide, which displays some information about a variety of incredible cars. The data I would need is a picture, video, make/model, top speed, short description, and price for each car I include. I will use the YouTube API (https://developers.google.com/youtube/v3) to pull the videos of the cars, as these would be very inefficient to store locally. The website might include a home page, which includes a bit of all the following as well as an about section, an "All Cars" page, which users could use to see all of the cars in my website, with functions to perhaps filter the cars by the available data, and a blog page, similar to the Adopt-A-Dog blog page from the last HTML class. The reason I want to create this website is I'm very interested in cool cars. With this website, I could create a convenient way to share my passion of cars with others (especially with the blog) in a cool and hopefully practical way.

Pages: Landing: summary, technology used, about the author, etc.
Cars Blog: You can make a Post about something.
All cars page: Allows the user to cycle through all cars, uses the API.
Resources page: Page that provides links to other pages where more resources can be found.

As I started to work on this project, I found I had a really hard time finding an API that was useful for what I wanted to do. My ideal choice of API (https://supercarsapi.docs.apiary.io/#) unfortunately
only supported one car. I did some more research online and found that the standard API recommended for beginners was to a a weather project. It is for that reason who I came up with Weather-Global. I used 
three APIs. First, MetaWeather (https://www.metaweather.com/) for the weather forecasts. Next, I used Teleport (https://teleport.org/) for city images. Lastly, I used my own Python API to manage blog posts.

This is the new structure of pages:
Home: Welcomes users to the site, uses minimal versions of the cities and blog pages to show features. Needed good modularity to do this.
Cities: Shows weather for all cities which I display.
Blog: Allows users to share their thoughts about the weather.
About Me: I'll brag about myself and the website I made for potential employers here.