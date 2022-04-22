# Youtube-data-analyse

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df=pd.read_csv(r'C:\Users\hp\Desktop\INvideos.CSV')
df
df.columns
df.isnull().any()

df['description']=df['description'].fillna(value='')
df

# df.info()


cdf=df['trending_date'].apply(lambda x:'20'+x[:2]).value_counts().to_frame().reset_index().rename(columns={"index":"year","trending_date":"no_of_videos"})
cdf


plt.bar(cdf['year'],cdf['no_of_videos'])
plt.show()

# what is the percentage of videos released in that particular year
cdf=df['trending_date'].apply(lambda x:'20'+x[:2]).value_counts(normalize=True)
cdf


df.describe()

# df.hist('views')

df[df['views']<1e6]['views'].count()/df['views'].count()*100

# df.hist('likes')

df[df['likes']<5000]['likes'].count()/df['likes'].count()*100

# df.hist('dislikes')
df[df['dislikes']<5000]['dislikes'].count()/df['dislikes'].count()*100

df.hist('comment_count')
df[df['comment_count']<5000]['comment_count'].count()/df['comment_count'].count()*100



df['title_length']=df['title'].apply(lambda x : len (x))
# df.columns
df.head(4)

df.boxplot('title_length')
plt.show()

plt.scatter(df['title_length'],df['views'])

# df.corr()

# grouping of data based on categery ID
df.groupby('category_id').sum()

# which category has highest views 
plt.bar(df['category_id'],df['views'])












