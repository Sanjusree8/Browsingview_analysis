#!/usr/bin/env python
# coding: utf-8
#execute code in spyder or jupyter 
# In[1]:


import json
import matplotlib.pyplot as plt      #importing all libraries
import pandas as pd
import numpy as np
import seaborn as sb


# In[2]:


import json
with open("C:/Users/Sanjana/Desktop/data (1).json") as f:  # loading the data file
    data = json.load(f)


# In[3]:


d=data['logs']
df=pd.DataFrame(d)        #creating a dataframe


# In[4]:


df.head()                       #return to top


# In[5]:


from datetime import datetime as dt
df['time'] =  [dt.fromtimestamp(int(date)/1000) for date in df['timestamp']]   #convert the unix ts


# In[6]:


ip=df.ip.value_counts().index                   #


# In[7]:


counts=df.ip.value_counts().values


# In[8]:


ip_df=pd.DataFrame()


# In[9]:


ip_df['ip']=ip


# In[10]:


ip_df['counts']=counts


# In[11]:


ip_df


# In[12]:


l=len(ip_df)
import numpy as np
values=np.arange(1,l+1)                       


# In[13]:


ip_df['values']=values


# In[14]:


d={}
for i,j in zip(ip_df['ip'],ip_df['counts']):
    d[i]=j


# In[15]:


df['ip_nm']=df['ip'].apply(lambda v: d[v])


# In[17]:


sb.lmplot(data=df,x='time',y='ip_nm',fit_reg=False,hue='ip',size=10,aspect=1.1)         


# In[ ]:


df['Tsp'] = pd.to_datetime(df['time']) 
df['Date'] =df['time'].dt.date 
df['Month'] =df['time'].dt.month 
df['Day'] = df['time'].dt.day     
df['Hour'] =df['time'].dt.hour   
df["Weekday"] = df['time'].dt.dayofweek 
df['Time']=df['time'].dt.time


# In[ ]:


df.head()           #returns to top


# In[ ]:


j=sb.jointplot(data=df,x='Hour',y='ip_nm')                        


# In[ ]:


sb.set_style("whitegrid")
sb.FacetGrid(df,hue='ip',size=10).map(plt.scatter,'Time','ip_nm')                  #graph
plt.show()


# In[ ]:


sb.set_style("whitegrid")
sb.FacetGrid(df,hue='ip',size=10).map(plt.scatter,'Hour','ip_nm').add_legend()        #graph
plt.show()







