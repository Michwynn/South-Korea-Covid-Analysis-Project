# South-Korea-Covid-Analysis-Project

Inspired by https://www.kaggle.com/datasets/kimjihoo/coronavirusdataset, you may find the relevant datasets and connections here.

This notebook is kind of messy but I have enumerated my observations of the dataset below and the approach I took towards understanding the datasets better. 

**Observations**

So with the south Korean dataset, I tried to see if there was any correlation between age and rate of being deceased. So I used the time_age dataset to derive the insight for this, using the split apply combine pattern in pandas through the groupby function, indexing on the date and age and then summing the data by the number of confirmed and deceased people. I also had to clean the column on age, removing the s and just using the integers. In calculating the correlation coefficient, pandas make it very easy so I applied the corr. Function on two column arrays and found the coefficient to be at 0.76 which is a positive and relatively strong relationship. And it makes sense, the older we are, the more likely that covid impacts an individual’s health more. 


But I also note that one of elements missing here, that would allow us to reach a more meaningful conclusion in terms of the correlation, would be the underlying conditions of these groups of elderly people, because it isn’t enough to say that just because one is older, that one will have a much higher chance of dying from covid, although in general that’s the case, I think it would be much more accurate to say that if one is older and he or she has underlying conditions such as pneumonia, then one have a much higher chance of dying because of covid, we have seen that underlying conditions are a much more accurate indicator of the effect of covid on an individual’s health because we see young people dying of covid too. In general I think this is meaningful relationship observed in the south Korean dataset, I wish the time period would’ve been longer to see if the linear relationship strengthens or weakens. 


Another correlation I tried finding was between average temperature and the no of covid cases. So I first used a graph that has two y axis to plot the no of confirmed cases in seoul and the average temperature in seoul through time, and the line chart showed that as average temperature increase, the no of confirmed cases also increased, that was just for seoul, I tried to see plot the same chart in another province jaellobuk and it also showed me pretty much the same thing. However, when I did the observation on a consolidated level, meaning plotting the confirmed cases in their respective province at the respective province’s average temperature, and I did this on a scatterplot matrix, it showed me that the positive correlation relationship was in fact spurious. 


So as a data scientist, I should always look at the data from different angles through grouping and segmentation. Effectively, I resolved Simpson’s Paradox. I noticed a trend appears in several groups of data by way of provinces but completely reverses when the province groups are combined, so that’s one casual story that could be told if we are not careful in our analysis. 

Another analysis I did of the covid-19 dataset was trying to determine the pattern of population movement within seoul. So the seoulfloating_df gives us the information and it contains a few columns, one as the date and another the floating population number and the rest of the columns are variables that describe that population such as the city and gender of that floating population and etc. So if I was interested to see as a whole, how do the residents living in seoul move in and out of the province, and then perhaps conduct further analysis by understanding whether the weather in seoul prompt a movement out of the province, so analysis of that nature. So using pandas I did a groupby on the date, and I applied the agg function based on the sum of total floating population. And then through the resulting groupby, I just directly call a plot function on it to see how the line graph looks, and apparently there is a huge spike and a couple of dips – both of which demand more than just a simple migration explanation, because the fluctuations are so extreme. Generally what we would expect is a line that fluctuates within a reasonable standard deviation, but the mean of that line should be straight line, and it wasn’t. I’ve tried cleaning it by looking at the variables that are actually causing the spike or dips, even if the values are too drastically different from previous. So for that dataset, through the split-apply-combine and visualisation, I managed to clean it fairly well, and through visual inspection, average temperature throughout the same period kept rising and has no influence or correlation to floating population fluctuations. 

Another example was to understand whether there is a correlation between temperature and no of covid cases within seoul and then within korea itself. So I had to leverage on the region_df, grouping dates as well as cities together and taking the sum of the confirmed, deceased and released numbers, put that in a dataframe, take the weather, do a groupby as well on date as well city and then use that dataframe to join with the region dataframe on both the indexes. So the analysis show that if I filter just for seoul, it would show as the average temperature rises, the no of confirmed cases rises as well, but if we do a scatterplot on all cities, we would find there is very little correlation between the temperature, wind speed on the no of confirmed covid cases, so I guess the maxim here is do not perceive noise as signals in the data because if we aggregate the data differently, it will show that the results could be due to randomness and I effectively resolved simpson’s paradox.

**In terms of the visualisation:**

The basic plot that I will like to highlight would be using matplotlib to create a time series chart comparing both cumulative covid cases in the country and the search volume of the word “coronavirus” against time. The idea behind this chart is to express to users that through time, people get more aware and educated about the virus and thus resulting in lower search volume even though cumulative confirmed covid cases are still rising. 


So we have both variables are encoded as quantitative variables and the chart is marked as a line pattern with encoded with 2 y-axes. So the left y-axis will be the cumulative covid confirmed cases and the right y-axis will be the search volume of the word coronavirus. On the x-axis we encoded date variable. So its very clear to the audience that both lines move in completely opposite direction, with cumulative covid confirmed cases always on the increase and the daily search volume decreases from 3rd march to 1st July 2020. 


The colour encoding of both lines are red and blue, red for cumulative confirmed cases and blue for coronavirus search volume, additionally the 2 variables orr both lines are encoded differently with an x shape for covid cases and o shape for search volume. So in terms of viewer perception – it really helps differentiate both lines. The axes are also positioned evenly although the 2 y-axes are of different scales. In terms of expressiveness, the graph is expressive and shows the correlation between the 2 variables. It tells the user immediately that as the cumulative confirmed covid cases rise, the daily search volume gradually decreases. 
In terms of effectiveness, users are able perceive the information rather easily with the aid of a legend the x axis in the appropriate date format so audience understand this is time series, adding a title stating that through time people are more aware of coronavirus with lesser daily search volume. Therefore, the graph very effective as it makes easy for users to perceive and decode the information as intended and quickly. 


For the advanced plot, I wanted to create a visual to show the audience the extent of the spread of covid infections in Korea so I created a geospatial visualisation to allow users to see where the confirmed and deceased covid cases are in Korea. Using geopandas, I layered scatterplots based on the longtitudes and latitudes of the confirmed and deceased cases of the cities in korea. so again using the grammar of graphics - the confirmed numbers by cities and the deceased numbers by cities” are both encoded as quantitative variables. The colour encoding used here also helps users identify cities that are infected, the map is light green with the borders of the provinces in dark grey, so users can easily differentiate the provinces and areas in korea, and the confirmed cases in black shape of filled circles and deceased numbers in red shape of filled circles. So essentially the map and scatterpoints are tell the users where the confirmed and deceased numbers are in korea and their relative concentrations, and since ive encoded the filled points to the quantitative variables, ive also used the size of the filled points as an indication, so the bigger the points are, the higher the deceased and confirmed numbers are in that area. I have also annoted the names of cities for some of the regions with highly concentrated numbers, but to avoid expressing too much information, I did not annotate the names of all the cities. So in terms of expressiveness, its not fully expressive. In terms of the human perception system, the graph is also less effective because we are worse at comparing relative numbers in terms of shape areas. But ive added in the chart title, a legend for easier readability, but in general I think the advanced plot does allow for users to have an idea of the various covid concentrated areas, and how much covid has spread throughout the country. So yes those are the 2 plots, among many, that were created for EDA of the datasets. 
