
# Heroes Of Pymoli Data Analysis

# purchase_data.json 
    # OBSERVED TREND 1   
        Approximately 81% of the purchasers are Male
    # OBSERVED TREND 2
        Top Age bucket for Purchasers is 20-24 (both in terms of Volume and Dollar Amount)
    # OBSERVED TREND 3
        Most popular items (based on Purchase count) : Betrayal, Whisper of Grieving Widows, Arcane Gem
        Most profitable item (based on total amount) : Retribution Axe 

# purchase_data2.json 
    # OBSERVED TREND 1   
        Approximately 81% of the purchasers are Male
    # OBSERVED TREND 2
        Top Age bucket for Purchasers is 20-24 (both in terms of Volume and Dollar Amount)
    # OBSERVED TREND 3
        Most popular items (based on Purchase count) : Mourning Blade
        Most profitable item (based on total amount) : Mourning Blade



```python
#Import statments for required Packages
import os
import json
import pprint
import pandas as pd
import numpy
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"
```


```python
#Open the JSON file and quick look on the data it contains.
file = os.path.join('Resources', 'purchase_data2.json')
json_df = pd.read_json(file)
json_df.head()
json_df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>78.000000</td>
      <td>78.000000</td>
      <td>78.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>22.551282</td>
      <td>93.935897</td>
      <td>2.924359</td>
    </tr>
    <tr>
      <th>std</th>
      <td>7.339003</td>
      <td>56.352633</td>
      <td>1.134913</td>
    </tr>
    <tr>
      <th>min</th>
      <td>7.000000</td>
      <td>0.000000</td>
      <td>1.020000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>20.000000</td>
      <td>48.000000</td>
      <td>1.925000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>22.500000</td>
      <td>97.500000</td>
      <td>2.770000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>25.000000</td>
      <td>137.000000</td>
      <td>4.092500</td>
    </tr>
    <tr>
      <th>max</th>
      <td>40.000000</td>
      <td>181.000000</td>
      <td>4.810000</td>
    </tr>
  </tbody>
</table>
</div>



# Player Count


```python
# Find the unique player count. 
unique_players = json_df["SN"].unique()
player_count = len(unique_players)
player_count_df = pd.DataFrame([{'Total Players' : player_count}])
player_count_df


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>74</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis (Total)


```python
#create lists to contain the required values
#unique items count
unique_Items_count = len(json_df["Item ID"].unique())
#Average Price
avg_pur_price = json_df["Price"].mean()
#total number of purchases
total_purchases = json_df["SN"].count()
#total purchase amount
total_revenue = json_df["Price"].sum()

#create a Dataframe 
purchasing_Analysis_PD = pd.DataFrame({
    "Number of Unique Items": [unique_Items_count],
    "Average Price": [avg_pur_price],
    "Number of Purchases": [total_purchases],
    "Total Revenue": [total_revenue]
})

#rearrage the Data frame attributes
purchasing_Analysis_PD = purchasing_Analysis_PD [[
    "Number of Unique Items",
    "Average Price",
    "Number of Purchases",
    "Total Revenue"
    
]]

#format the price and revenue columns to $
purchasing_Analysis_PD["Average Price"] = purchasing_Analysis_PD["Average Price"].map("${0:,.2f}".format)
purchasing_Analysis_PD["Total Revenue"] = purchasing_Analysis_PD["Total Revenue"].map("${0:,.2f}".format)



purchasing_Analysis_PD
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>64</td>
      <td>$2.92</td>
      <td>78</td>
      <td>$228.10</td>
    </tr>
  </tbody>
</table>
</div>



# Gender Demographics


```python
#total players under each gender
gender_count = json_df.groupby("Gender")["SN"].nunique()
#% of players in each enger
gender_percent = (gender_count / sum(gender_count)) * 100

#join the series into a disctionary
gender_demographics = {
    "Percentage of Players" : gender_percent ,
    "Total Count" : gender_count
}

#convert to a dataframe
gender_demographics_DF = pd.DataFrame(gender_demographics)
#use round() to format the values
gender_demographics_DF = gender_demographics_DF.round(2)
gender_demographics_DF 

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>17.57</td>
      <td>13</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>81.08</td>
      <td>60</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1.35</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis (Gender)


```python
#group the data set by "gender"
gender_group = json_df.groupby("Gender")
#total purhchases for each gender
gender_purchase_count = gender_group["Item ID"].count()
#average purchase price for each gender
gender_purchase_avg = gender_group["Price"].mean()
#total purchase price for each gender
gender_purchase_tot = gender_group["Price"].sum()
#normalized proce : total_price / unique number of users
gender_purchase_nor = gender_group["Price"].sum() /gender_demographics_DF["Total Count"]

#join the series into a dictionary
gender_analysis = {
    "Purchase Count" : gender_purchase_count,
    "Average Purchase Price" : gender_purchase_avg,
    "Total Purchase Value" : gender_purchase_tot,
    "Normalized Totals" : gender_purchase_nor
}

#convert to a datafram
gender_analysis_DF = pd.DataFrame(gender_analysis)

#rearrage columns to make DF presentable
gender_analysis_DF = gender_analysis_DF[[
    "Purchase Count",
    "Average Purchase Price",
    "Total Purchase Value",
    "Normalized Totals"
]]

#format the required columns 
gender_analysis_DF["Average Purchase Price"] = gender_analysis_DF["Average Purchase Price"].map("${0:,.2f}".format)
gender_analysis_DF["Total Purchase Value"] = gender_analysis_DF["Total Purchase Value"].map("${0:,.2f}".format)
gender_analysis_DF["Normalized Totals"] = gender_analysis_DF["Normalized Totals"].map("${0:,.2f}".format)

gender_analysis_DF


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>13</td>
      <td>$3.18</td>
      <td>$41.38</td>
      <td>$3.18</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>64</td>
      <td>$2.88</td>
      <td>$184.60</td>
      <td>$3.08</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1</td>
      <td>$2.12</td>
      <td>$2.12</td>
      <td>$2.12</td>
    </tr>
  </tbody>
</table>
</div>



# Age Demographics


```python
# create the required bins
bins = [0, 10, 15, 20, 25 , 30, 35, 40, 100]
#labels for thes bins
group_names = ['<10', '10-14', '15-19', '20-24' , '25-29' , '30-34', '35-39' , '40+']
#cut the data frame into bins based on the Age column
json_df["Age Bin"] =  pd.cut(json_df["Age"], bins, labels=group_names)

#total players in each age bin
player_count = json_df["Age Bin"].value_counts()
#percentage of players in each ageb bin
player_per = player_count / len(json_df) * 100

#create a list of dictionary
age_demographics = {
    "Percentage of Players" : player_per ,
    "Total Count" : player_count
}

#convert to Dataframe
age_demographics_DF = pd.DataFrame(age_demographics)
#format required columns
age_demographics_DF = age_demographics_DF.round(2)
age_demographics_DF


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20-24</th>
      <td>42.31</td>
      <td>33</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>25.64</td>
      <td>20</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>8.97</td>
      <td>7</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>6.41</td>
      <td>5</td>
    </tr>
    <tr>
      <th>&lt;10</th>
      <td>6.41</td>
      <td>5</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>5.13</td>
      <td>4</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>5.13</td>
      <td>4</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>0.00</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis (Age)


```python
#group the data set based on the Age bin
Age_group = json_df.groupby("Age Bin")
#len(gender_group["Item ID"])

#calculations to create lists of values for each bin
age_purchase_count = Age_group["Item ID"].count()
age_purchase_unique_count = Age_group["SN"].nunique()
age_purchase_avg = Age_group["Price"].mean()
age_purchase_tot = Age_group["Price"].sum()
age_purchase_nor = Age_group["Price"].sum() / age_purchase_unique_count
 
#join the lists into discitonary
age_analysis = {
    "Purchase Count" : age_purchase_count,
    "Average Purchase Price" : age_purchase_avg,
    "Total Purchase Value" : age_purchase_tot,
    "Normalized Totals" : age_purchase_nor   
}

#convert to a dataframe
age_analysis_DF = pd.DataFrame(age_analysis)

#rearrange the DF to make it presentable
age_analysis_DF = age_analysis_DF[[
    "Purchase Count",
    "Average Purchase Price",
    "Total Purchase Value",
    "Normalized Totals"
]]

#frmat the required columns
age_analysis_DF["Average Purchase Price"] = age_analysis_DF["Average Purchase Price"].map("${0:,.2f}".format)
age_analysis_DF["Total Purchase Value"] = age_analysis_DF["Total Purchase Value"].map("${0:,.2f}".format)
age_analysis_DF["Normalized Totals"] = age_analysis_DF["Normalized Totals"].map("${0:,.2f}".format)

age_analysis_DF



```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
    <tr>
      <th>Age Bin</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>5</td>
      <td>$2.76</td>
      <td>$13.82</td>
      <td>$2.76</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>4</td>
      <td>$3.05</td>
      <td>$12.21</td>
      <td>$3.05</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>20</td>
      <td>$2.73</td>
      <td>$54.69</td>
      <td>$2.73</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>33</td>
      <td>$3.04</td>
      <td>$100.42</td>
      <td>$3.35</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>4</td>
      <td>$2.69</td>
      <td>$10.77</td>
      <td>$2.69</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>7</td>
      <td>$2.35</td>
      <td>$16.47</td>
      <td>$2.75</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>5</td>
      <td>$3.94</td>
      <td>$19.72</td>
      <td>$3.94</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>0</td>
      <td>$nan</td>
      <td>$0.00</td>
      <td>$nan</td>
    </tr>
  </tbody>
</table>
</div>



# Top Spenders


```python
#create a join data set based on SN
Spender_group = json_df.groupby("SN")

#calcualte the lists for total purchases , average_spend, total_spend
Spender_purchase_count = Spender_group["Item ID"].count()
Spender_purchase_avg = Spender_group["Price"].mean()
Spender_purchase_tot = Spender_group["Price"].sum()

#convert into a dictionary
spender_analysis = {
    "Purchase Count" : Spender_purchase_count,
    "Average Purchase Price" : Spender_purchase_avg,
    "Total Purchase Value" : Spender_purchase_tot  
}

#convert into a dataframe
spender_analysis_DF = pd.DataFrame(spender_analysis)
#rearrange the columns 
spender_analysis_DF = spender_analysis_DF[[
    "Purchase Count",
    "Average Purchase Price",
    "Total Purchase Value"
]]

#format the reqired columns
spender_analysis_DF["Average Purchase Price"] = spender_analysis_DF["Average Purchase Price"].map("${0:,.2f}".format)
spender_analysis_DF["Total Purchase Value"] = spender_analysis_DF["Total Purchase Value"].map("${0:,.2f}".format)

#sort in Descending order, this will help to display top spender
spender_analysis_DF = spender_analysis_DF.sort_values(by="Purchase Count", ascending=False)

#display first 5 records : top 5 spenders
spender_analysis_DF.head(5)

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aidaira26</th>
      <td>2</td>
      <td>$2.56</td>
      <td>$5.13</td>
    </tr>
    <tr>
      <th>Chaniman66</th>
      <td>2</td>
      <td>$1.61</td>
      <td>$3.23</td>
    </tr>
    <tr>
      <th>Hairith93</th>
      <td>2</td>
      <td>$2.12</td>
      <td>$4.25</td>
    </tr>
    <tr>
      <th>Sundaky74</th>
      <td>2</td>
      <td>$3.71</td>
      <td>$7.41</td>
    </tr>
    <tr>
      <th>Aeri79</th>
      <td>1</td>
      <td>$4.15</td>
      <td>$4.15</td>
    </tr>
  </tbody>
</table>
</div>



# Most Popular Items


```python
#calculations to create lists for item_price, item_count, total_price
item_price = json_df.groupby(['Item ID', 'Item Name'])['Price'].min()
item_count = json_df.groupby(['Item ID', 'Item Name'])['SN'].count()
item_totPrice = json_df.groupby(['Item ID', 'Item Name'])['Price'].sum()

#create dictionary
popular_analysis = {
    "Purchase Count" : item_count,
    "Item Price" : item_price,
    "Total Purchase Value" : item_totPrice 
}

#create dataframe
popular_analysis_DF = pd.DataFrame(popular_analysis)
#rearrange columns
popular_analysis_DF = popular_analysis_DF[[
    "Purchase Count",
    "Item Price",
    "Total Purchase Value"
]]

#sort the dataframe in descednding order to diplay popular items based on the items sold
popular_analysis_DF = popular_analysis_DF.sort_values(by="Purchase Count", ascending=False)
#display first 5 records : top 5 popular items
popular_analysis_DF.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>94</th>
      <th>Mourning Blade</th>
      <td>3</td>
      <td>3.64</td>
      <td>10.92</td>
    </tr>
    <tr>
      <th>90</th>
      <th>Betrayer</th>
      <td>2</td>
      <td>4.12</td>
      <td>8.24</td>
    </tr>
    <tr>
      <th>111</th>
      <th>Misery's End</th>
      <td>2</td>
      <td>1.79</td>
      <td>3.58</td>
    </tr>
    <tr>
      <th>64</th>
      <th>Fusion Pummel</th>
      <td>2</td>
      <td>2.42</td>
      <td>4.84</td>
    </tr>
    <tr>
      <th>154</th>
      <th>Feral Katana</th>
      <td>2</td>
      <td>4.11</td>
      <td>8.22</td>
    </tr>
  </tbody>
</table>
</div>



# Most Profitable Items


```python
#sort the dataframe in descednding order to diplay popular items based on the total purchase value
popular_analysis_DF = popular_analysis_DF.sort_values(by="Total Purchase Value", ascending=False)
#display first 5 records : top 5 profitable items
popular_analysis_DF.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>94</th>
      <th>Mourning Blade</th>
      <td>3</td>
      <td>3.64</td>
      <td>10.92</td>
    </tr>
    <tr>
      <th>117</th>
      <th>Heartstriker, Legacy of the Light</th>
      <td>2</td>
      <td>4.71</td>
      <td>9.42</td>
    </tr>
    <tr>
      <th>93</th>
      <th>Apocalyptic Battlescythe</th>
      <td>2</td>
      <td>4.49</td>
      <td>8.98</td>
    </tr>
    <tr>
      <th>90</th>
      <th>Betrayer</th>
      <td>2</td>
      <td>4.12</td>
      <td>8.24</td>
    </tr>
    <tr>
      <th>154</th>
      <th>Feral Katana</th>
      <td>2</td>
      <td>4.11</td>
      <td>8.22</td>
    </tr>
  </tbody>
</table>
</div>


