## What Plane is the Safest?

This project used the airplane crashes since 1908 data set from Kaggle. 
Data was analyzed to answer the following questions:
What is the probability of dying if a plane crashes?
What is the safest type of plane to travel on?
Are there bad dates to travel?

# Data

If the number of passengers aboard the plane or fatalities were null the rows were dropped from the data set.
A risk of death feature was created by dividing flight fatalities by total passengers aboard.
The crashed flights were split into 5 groups based on their operator. Anything that contained military was classified as a military flight. Operators containing ‘private’ were classified as private flights. The rest of the flights were divided into small (less than 30 passengers), medium (more than 29 but less than 200 passengers), and large (more than 200 passengers). 

#Data Exploration

The risk of dying in a crash is highest for military and gets lower the larger the aircraft is. With the mean of a large plane having a 50% chance you will die, the smaller the plane gets the higher the average of fatality. This data is summarized below in the table and detailed in the scatter plot below.

Flight type and   chance of death

Military    93%
Private     86%
Small       85%
Medium      71%
Large       50%

Flight type  |  Chance of 100% Fatality | Your Chance of Fatality
Military     | 77%                      | 93%
Private      | 75%                      | 86%
Small        | 71%                      | 85%
Medium       | 47%                      | 71%
Large        | 36%                      | 50%

This table shows the risk that everyone on the plane will die in a crash. About 1 out of three large planes result in 100% fatalities, and almost half of medium planes do. The other categories have 3/4 of crashes resulting in 100% fatalities. You can also see this in the histograms.
So, your chance of dying in a large plane crash or we could say normal commercial flight is about a coin toss. However, the probability that everyone will die is 1/3. So, you have a 50% chance of death, but everyone together only have a 1/3 chance of death. You can apply these statistics to the rest of the categories.

You should remember that large flights usually have everyone die or everyone survive, but if you ever find yourself in need of hope in a plane crash you should remember both outlooks.


To our final question, are some days or times more dangerous than others?

When airplanes were first invented in the early 1900s there was not much data on plane crashes, but by the 1930s the average rate of death in a crash and standard deviation started to normalize.
It does not look like the time of day, month, or year significantly affects the risk of death.
So, book that red eye, evening, or mid-morning flight, you will be equally safe.

# Conclusion

You should remember that this data set does not show how likely you will die traveling by plane. This data shows how likely you will die/survive if the plane you are on happens to crash. If your plane isn’t going to crash, you should be fine. None of the factors that caused these plane crashes was analyzed either, so looking into that would be a follow-up to this project. 

This data set also is not optimized to use for locational data. There are about 5000 rows in this data set and there are 4304 unique locations, so looking at the locations would not help unless we simplified them into countries or regions. Likewise, we cannot see what planes are safest to ride in because this dataset only contains plane models and types that have crashed. Any plane that is not in this data set is statistically the safest to ride in.


