# Ex-09-Data-Visualization-II

## AIM
To Perform Data Visualization on a complex dataset and save the data to a file. 

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
### STEP 1
Read the given Data
### STEP 2
Clean the Data Set using Data Cleaning Process
### STEP 3
Apply Feature generation and selection techniques to all the features of the data set
### STEP 4
Apply data visualization techniques to identify the patterns of the data.
# PROGRAM:

Developed by: KAVYA K
Register no: 212222230065
# CODE
## loading the dataset
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("Superstore.csv")
df
```
## removing unnecessary data variables
```
df.drop('Row ID',axis=1,inplace=True)
df.drop('Order ID',axis=1,inplace=True)
df.drop('Customer ID',axis=1,inplace=True)
df.drop('Customer Name',axis=1,inplace=True)
df.drop('Country',axis=1,inplace=True)
df.drop('Postal Code',axis=1,inplace=True)
df.drop('Product ID',axis=1,inplace=True)
df.drop('Product Name',axis=1,inplace=True)
df.drop('Order Date',axis=1,inplace=True)
df.drop('Ship Date',axis=1,inplace=True)
print("Updated dataset")
df

df.isnull().sum()
```
## detecting and removing outliers in current numeric data
```
plt.figure(figsize=(12,10))
plt.title("Data with outliers")
df.boxplot()
plt.show()

plt.figure(figsize=(12,10))
cols = ['Sales','Quantity','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
```
## data visualization
## line plots
## import seaborn as sns
```
sns.lineplot(x="Sub-Category",y="Sales",data=df,marker='o')
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.lineplot(x="Category",y="Profit",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Categories vs Profit")
plt.show()

sns.lineplot(x="Region",y="Sales",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Region area vs Sales")
plt.show()

sns.lineplot(x="Category",y="Discount",data=df,marker='o')
plt.title("Categories vs Discount")
plt.show()

sns.lineplot(x="Sub-Category",y="Quantity",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Sub Categories vs Quantity")
plt.show()
## bar plots
sns.barplot(x="Sub-Category",y="Sales",data=df)
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Profit",data=df)
plt.title("Categories vs Profit")
plt.show()

sns.barplot(x="Sub-Category",y="Quantity",data=df)
plt.title("Sub Categories vs Quantity")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Discount",data=df)
plt.title("Categories vs Discount")
plt.show()

plt.figure(figsize=(12,7))
sns.barplot(x="State",y="Sales",data=df)
plt.title("States vs Sales")
plt.xticks(rotation = 90)
plt.show()

plt.figure(figsize=(25,8))
sns.barplot(x="State",y="Sales",hue="Region",data=df)
plt.title("State vs Sales based on Region")
plt.xticks(rotation = 90)
plt.show()
```
## Histogram
```
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()
```
## count plot
```
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')
```
## Barplot
```
sns.boxplot(x="Sub-Category",y="Discount",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot( x="Profit", y="Category",data=df)
plt.xticks(rotation = 90)
plt.show()
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Profit",data=df)
sns.boxplot(x="Region",y="Sales",data=df)
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Quantity",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Discount",data=df)
plt.figure(figsize=(15,7))
sns.boxplot(x="State",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
```
## KDE plot
```
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')
```
## violin plot
```
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)
```
## point plot
```
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])
```
## Pie Chart
```
df.groupby(['Category']).sum().plot(kind='pie', y='Discount',figsize=(6,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Sub-Category']).sum().plot(kind='pie', y='Sales',figsize=(10,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Region']).sum().plot(kind='pie', y='Profit',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Ship Mode']).sum().plot(kind='pie', y='Quantity',figsize=(8,11),pctdistance=1.7,labeldistance=1.2)

df1=df.groupby(by=["Category"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)  
plt.figure(figsize=(8,8))
colors = sns.color_palette('pastel')
plt.pie(df1["Profit"],colors = colors,labels=labels, autopct = '%0.0f%%')
plt.show()

df1=df.groupby(by=["Ship Mode"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)
colors=sns.color_palette("bright")
plt.pie(df1["Sales"],labels=labels,autopct="%0.0f%%")
plt.show()
```
## HeatMap
```
df4=df.copy()
```
## encoding
```
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder,OneHotEncoder
le=LabelEncoder()
ohe=OneHotEncoder
oe=OrdinalEncoder()

df4["Ship Mode"]=oe.fit_transform(df[["Ship Mode"]])
df4["Segment"]=oe.fit_transform(df[["Segment"]])
df4["City"]=le.fit_transform(df[["City"]])
df4["State"]=le.fit_transform(df[["State"]])
df4['Region'] = oe.fit_transform(df[['Region']])
df4["Category"]=oe.fit_transform(df[["Category"]])
df4["Sub-Category"]=le.fit_transform(df[["Sub-Category"]])
```
## scaling
```
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])
 ```                                              
## Heatmap
```
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()
```
# OUPUT
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/4fac80f5-8944-4383-9cea-ff71744b650a)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/aa9f3fb3-afee-4818-b608-6d3e9f9edcd9)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/225c79a2-da8c-40fd-9185-1a35dd38a348)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/68f33ced-05e5-4ba3-b6a7-f1597b1ecf00)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/f03ef736-754c-4c83-81de-e58e9c99f957)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/81c9022c-781c-42d9-8a83-829ad72b396a)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/8035ab8f-a2b3-4b12-b57f-d787d027e69b)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/04f27f31-bfa2-46c1-bcd9-cf0fa4111019)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/11da11f2-8329-41ec-9bdf-887fe5ad90a1)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/f2497551-0f17-4998-9751-d8bf4a7d4305)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/a7763611-7751-4382-9630-1bef8cf6a6d1)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/5db0ae0e-d708-42e0-af8e-b3ba4081f157)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/e0fc111c-533d-4fc5-90be-3679023c2f88)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/807e05b0-173a-4f17-8d98-3f96070057f4)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/2c9ab7a4-1d5d-4bc6-b2e9-75f9f209b9b5)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/516d3695-cad2-4a61-b0b6-72fdaaffac1e)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/493caecc-b40c-4ccd-bb71-7f930b6dc3fc)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/69199d21-9edf-4962-93b7-9537efc45041)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/d141ab91-e050-45b1-afb3-b187e22e937e)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/65e9ff98-e8ef-44e7-a0fd-e0a91529f4f9)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/e2dda05b-d27a-4f3b-b808-9688281204c2)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/844848b0-0f2a-4af0-a92f-fe7cfa02b616)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/903c9ffe-39ea-4fc7-8d16-4a1c5d96eff1)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/f87378e6-ccbf-4d87-b3e7-d55be574c59f)
![image](https://github.com/kavyasenthamarai/Ex-08-Data-Visualization_1/assets/118668727/594154d6-d769-4922-991e-9b01c63bbc2a)
# Result:
Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file
