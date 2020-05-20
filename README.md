# Houses_Sales_Data_Analysis_IBM
# -*- coding: utf-8 -*-
"""
Created on Sat May  9 20:38:33 2020

@author: 31685
"""

# import pandas library
import pandas as pd

# Read the online file by the URL provides above, and assign it to variable "df"
other_path = "https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/DA0101EN/auto.csv"
df = pd.read_csv(other_path, header=None)
# show the first 5 rows using dataframe.head() method
#print("The first 5 rows of the dataframe") 
#print(df.head(5))

#1: check the bottom 10 rows of data frame "df".

#<!-- The answer is below:

#print("The last 10 rows of the dataframe\n")
#print(df.tail(10))

# create headers list
headers = ["symboling","normalized-losses","make","fuel-type","aspiration", "num-of-doors","body-style",
         "drive-wheels","engine-location","wheel-base", "length","width","height","curb-weight","engine-type",
         "num-of-cylinders", "engine-size","fuel-system","bore","stroke","compression-ratio","horsepower",
         "peak-rpm","city-mpg","highway-mpg","price"]

#print("headers\n", headers)
df.columns = headers
#print(df.head(10))

df.dropna(subset=["price"], axis=0)
print(df.columns)
#datayi pc ye kaydettik 
df.to_csv("automobile.csv", index=False)

# check the data type of data frame "df" by .dtypes
print(df.dtypes)


print(df.describe())

# describe all the columns in "df" 
#print(df.describe(include = "all"))

#3: You can select the columns of a data frame by indicating the name of each column, for example, you can select the three columns as follows:
#Apply the method to ".describe()" to the columns 'length' and 'compression-ratio'.
dfnew=df[['length', 'compression-ratio']].describe()
#print(dfnew)

# look at the info of "df"
print(df.info)

# -*- coding: utf-8 -*-
"""
Created on Mon May 11 16:34:13 2020

@author: 31685
"""


import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

path='https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/DA0101EN/automobileEDA.csv'
df = pd.read_csv(path)
df.head()
df.corr()

# list the data types for each column
df.dtypes

#2: Find the correlation between the following columns: bore, stroke,compression-ratio , and horsepower.

#Hint: if you would like to select those columns use the following syntax: df[['bore','stroke' ,'compression-ratio','horsepower']]
#solution 
#df[['bore', 'stroke', 'compression-ratio', 'horsepower']].corr() 

# Engine size as potential predictor variable of price
#sns.regplot(x="engine-size", y="price", data=df)
#print(plt.ylim(0,))

#print(df[["engine-size", "price"]].corr())
#We can examine the correlation between 'engine-size' and 'price' and see it's approximately 0.87

#Highway mpg is a potential predictor variable of price
#sns.regplot(x="highway-mpg", y="price", data=df)
#We can examine the correlation between 'highway-mpg' and 'price' and see it's approximately -0.704
#(df[['highway-mpg', 'price']].corr()) 

#sns.regplot(x="peak-rpm", y="price", data=df)
#print(df[['peak-rpm','price']].corr())

sns.boxplot(x="body-style", y="price", data=df)
#Result: We see that the distributions of price between the different body-style categories have a significant overlap, and so body-style would not be a good predictor of price. Let's examine engine "engine-location" and "price":
sns.boxplot(x="engine-location", y="price", data=df)
#Result: Here we see that the distribution of price between these two engine-location categories, front and rear, are distinct enough to take engine-location as a potential good predictor of price.
sns.boxplot(x="drive-wheels", y="price", data=df)
#Result: Here we see that the distribution of price between the different drive-wheels categories differs; as such drive-wheels could potentially be a predictor of price.


print(df.describe())
print(df.describe(include=['object']))



#Value-counts is a good way of understanding how many units of each characteristic/variable we have.
#print(df['drive-wheels'].value_counts())
#We can convert the series to a Dataframe as follows :
#print(df['drive-wheels'].value_counts().to_frame())

#Let's repeat the above steps but save the results to the dataframe "drive_wheels_counts" and rename the column  'drive-wheels' to 'value_counts'.
#drive_wheels_counts = df['drive-wheels'].value_counts().to_frame()
#drive_wheels_counts.rename(columns={'drive-wheels': 'value_counts'}, inplace=True)
#print(drive_wheels_counts)
#Now let's rename the index to 'drive-wheels':
#drive_wheels_counts.index.name = 'drive-wheels'
#print(drive_wheels_counts)

#We can repeat the above process for the variable 'engine-location'.
# engine-location as variable
#engine_loc_counts = df['engine-location'].value_counts().to_frame()
#engine_loc_counts.rename(columns={'engine-location': 'value_counts'}, inplace=True)
#engine_loc_counts.index.name = 'engine-location'
#print(engine_loc_counts.head(10))




