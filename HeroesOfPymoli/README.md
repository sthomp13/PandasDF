
Congratulations! After a lot of hard work in the data munging mines, you've landed a job as Lead Analyst for an independent gaming company. You've been assigned the task of analyzing the data for their most recent fantasy game Heroes of Pymoli.

Like many others in its genre, the game is free-to-play, but players are encouraged to purchase optional items that enhance their playing experience. As a first task, the company would like you to generate a report that breaks down the game's purchasing data into meaningful insights.



```python
#Dependencies
import pandas as pd
import numpy as np
```


```python
#Save path to data set in a variable
data_file = "purchase_data.json"
data_file2 = "purchase_data2.json"

```


```python
#Use pandas to read the data
print(data_file)
#data_file_pd = pd.read_json(data_file)
pd_file = pd.read_json(data_file)
pd_file.head()
```

    purchase_data.json
    




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
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>



Purchasing Analysis (Total)


```python
players_count = len(pd_file["SN"].value_counts())
players_count
```




    573




```python
#Unique Number of Items
unique_purchases = len(pd_file["Price"].unique())
unique_purchases

```




    152




```python
price_mean = pd_file["Price"].mean()
price_mean
```




    2.931192307692303




```python
#Total Number of Prurchases
purch_count = len(pd_file["Price"])
purch_count
```




    780




```python
totalRev = sum(pd_file["Price"])
totalRev
```




    2286.3299999999963




```python
player_count = pd.DataFrame({"Player Count": players_count},
                           index = [0])
player_count
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
      <th>Player Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>573</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Convert series into DataFrams
purchaseAnalysis= pd.DataFrame({"Number of Unique Items": unique_purchases,
                           "Average Purchase Price": price_mean,
                           "Total Number of Purchases": purch_count,
                           "Total Revenue": totalRev},
                          index = [0])
purchaseAnalysis
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
      <th>Average Purchase Price</th>
      <th>Number of Unique Items</th>
      <th>Total Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2.931192</td>
      <td>152</td>
      <td>780</td>
      <td>2286.33</td>
    </tr>
  </tbody>
</table>
</div>



You must include a written description of three observable trends based on the data.

In the above dataframe, I see that the average price is 2.93 overall. The average purchase price for female was $2.81, $2.95 for men and $3.24 for other/non-disclosed. It appears that as a whole, women paid the least for the game. However, other/non-disclosed were willing to pay the most.

Unsurprisingly, men bought the most video games by far! Out of 780 purchases, men bought 633. That is roughly 81%! 

The total purchase value is also very high for men: $1,867.68. By contrast, the purchase value was only 382.91 for women. That is roughly a 79% difference. 

Overall, the independent gaming company should focus on marketing their products to men if they already aren't doing so to get the most sales and profit. Women only make up roughly 17% of purchases. 

Additionally, the most profitable item was Retribution Axe for 9 years old. The independent gaming company may also want to focus on selling this product in as many stores as possible.

Furthermore, the greatest purchase value was experience for 20 to 24 year olds. The independent gaming company may benefit from selling games in colleges, as a lot of students in college are in that age range.

# Gender Demographics


```python
#Gender Demographics
#Percentage and Counts of Male/Female Players
#Percentage and Counts of Other/Non-Disclosed
#same player can have multiple items 
male_count_1 = pd_file.groupby(["SN", "Gender"]).size()
#male_count_1.count().head()

players_1 = pd.DataFrame(male_count_1)
players_1
players_2 = pd.DataFrame(players_1.groupby(["Gender"]).count())
players_2.columns = ["GenderCount"]
players_2

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
      <th>GenderCount</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>100</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>465</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
players_male = players_2["GenderCount"].loc["Male"]
print(players_male)
```

    465
    


```python
male_percentage = round(players_male / player_count, 2) * 100
male_percentage
#male_percentage * 100
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
      <th>Player Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>81.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# female_players = len(pd_file.loc[pd_file["Gender"] == "Female"])
# female_players
female_players = players_2["GenderCount"].loc["Female"]
female_players
```




    100




```python
female_percentage = round(female_players / player_count, 2) * 100
female_percentage
#female_percentage * 100
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
      <th>Player Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>17.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# other_players = len(pd_file[pd_file["Gender"] == "Other / Non-Disclosed"])
# other_players
other_players = players_2["GenderCount"].loc["Other / Non-Disclosed"]
other_players
```




    8




```python
other_percentage = round(other_players / player_count, 2) * 100
other_percentage 
#other_percentage * 100
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
      <th>Player Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Convert series into DataFrames
genderDemo= pd.DataFrame({"Count of Male Players": players_male,
                           "Percent of Male Players": male_percentage,
                           "Count of Female Players": female_players,
                           "Percent of Female Players": female_percentage,
                           "Count of Other / Non-Disclosed": other_players,
                           "Percent of Other / Non-Disclosed": other_percentage},
        
                          index = [0])
genderDemo
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
      <th>Count of Female Players</th>
      <th>Count of Male Players</th>
      <th>Count of Other / Non-Disclosed</th>
      <th>Percent of Female Players</th>
      <th>Percent of Male Players</th>
      <th>Percent of Other / Non-Disclosed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>100</td>
      <td>465</td>
      <td>8</td>
      <td>17</td>
      <td>81</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis (Gender)


```python
#Gender Purchase Analysis
purchGender = pd_file.groupby(["Gender"])
purchGender.head()
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
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
    <tr>
      <th>7</th>
      <td>29</td>
      <td>Female</td>
      <td>169</td>
      <td>Interrogator, Blood Blade of the Queen</td>
      <td>3.32</td>
      <td>Iathenudil29</td>
    </tr>
    <tr>
      <th>16</th>
      <td>22</td>
      <td>Female</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>1.14</td>
      <td>Sundista85</td>
    </tr>
    <tr>
      <th>17</th>
      <td>22</td>
      <td>Female</td>
      <td>59</td>
      <td>Lightning, Etcher of the King</td>
      <td>1.65</td>
      <td>Aenarap34</td>
    </tr>
    <tr>
      <th>22</th>
      <td>11</td>
      <td>Female</td>
      <td>11</td>
      <td>Brimstone</td>
      <td>2.52</td>
      <td>Deural48</td>
    </tr>
    <tr>
      <th>29</th>
      <td>16</td>
      <td>Female</td>
      <td>45</td>
      <td>Glinting Glass Edge</td>
      <td>2.46</td>
      <td>Phaedai25</td>
    </tr>
    <tr>
      <th>177</th>
      <td>34</td>
      <td>Other / Non-Disclosed</td>
      <td>155</td>
      <td>War-Forged Gold Deflector</td>
      <td>3.73</td>
      <td>Assassa38</td>
    </tr>
    <tr>
      <th>209</th>
      <td>33</td>
      <td>Other / Non-Disclosed</td>
      <td>157</td>
      <td>Spada, Etcher of Hatred</td>
      <td>2.21</td>
      <td>Frichistasta59</td>
    </tr>
    <tr>
      <th>244</th>
      <td>21</td>
      <td>Other / Non-Disclosed</td>
      <td>183</td>
      <td>Dragon's Greatsword</td>
      <td>2.36</td>
      <td>Tyaerith73</td>
    </tr>
    <tr>
      <th>267</th>
      <td>33</td>
      <td>Other / Non-Disclosed</td>
      <td>65</td>
      <td>Conqueror Adamantite Mace</td>
      <td>1.96</td>
      <td>Frichistasta59</td>
    </tr>
    <tr>
      <th>276</th>
      <td>12</td>
      <td>Other / Non-Disclosed</td>
      <td>128</td>
      <td>Blazeguard, Reach of Eternity</td>
      <td>4.00</td>
      <td>Aillycal84</td>
    </tr>
  </tbody>
</table>
</div>




```python
gnpurcount = pd_file["Gender"].value_counts()
#gnpurcount = pd.DataFrame(purchGender[3].value_counts())
gnpurcount
```




    Male                     633
    Female                   136
    Other / Non-Disclosed     11
    Name: Gender, dtype: int64




```python
groupprice1 = purchGender["Price"].mean()
groupprice1
```




    Gender
    Female                   2.815515
    Male                     2.950521
    Other / Non-Disclosed    3.249091
    Name: Price, dtype: float64




```python
purchbygen = purchGender["Price"].sum()
purchbygen
```




    Gender
    Female                    382.91
    Male                     1867.68
    Other / Non-Disclosed      35.74
    Name: Price, dtype: float64




```python
normtotal = round(purchbygen/players_2["GenderCount"],2)
normtotal
```




    Gender
    Female                   3.83
    Male                     4.02
    Other / Non-Disclosed    4.47
    dtype: float64




```python
genderpa = pd.DataFrame({"Purchase Count":gnpurcount,
                        "Average Purchase Price":groupprice1,
                         "Total Purchase Value":purchbygen,
                          "Normalized Total": normtotal} )
genderpa
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
      <th>Average Purchase Price</th>
      <th>Normalized Total</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>2.815515</td>
      <td>3.83</td>
      <td>136</td>
      <td>382.91</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>2.950521</td>
      <td>4.02</td>
      <td>633</td>
      <td>1867.68</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>3.249091</td>
      <td>4.47</td>
      <td>11</td>
      <td>35.74</td>
    </tr>
  </tbody>
</table>
</div>



# AGE DEMOGRAPHICS


```python
# Figuring out the maximum age can help with creating buckets. 
print(pd_file["Age"].max())
```

    45
    


```python
#Age Demographics
#Break into Bins of 4 Years
bins = [0, 9.9, 14.9, 19.9, 24.9, 29.9, 34.9, 39.9, 120]
group_names = ["<10", "10-14", "15-19", "20-24", "25-29",
             "30-34", "35-39", "40+"]
group_names
```




    ['<10', '10-14', '15-19', '20-24', '25-29', '30-34', '35-39', '40+']




```python
pd.cut(pd_file["Age"], bins, labels = group_names).head()
```




    0    35-39
    1    20-24
    2    30-34
    3    20-24
    4    20-24
    Name: Age, dtype: category
    Categories (8, object): [<10 < 10-14 < 15-19 < 20-24 < 25-29 < 30-34 < 35-39 < 40+]




```python
# pymoli_df["Age Group"] = pd.cut(pymoli_df["Age"], bins, labels=group_names)
pd.cut(pd_file["Age"], bins, labels = group_names)
pd_file["Age Range"] = pd.cut(pd_file["Age"], bins, labels = group_names)
pdages = pd_file.groupby(["SN","Age Range"])

                                                              
players = pd.DataFrame(pdages.size())
#players

agegroups = pd.DataFrame(players.groupby(["Age Range"]).count())
agegroups.columns= ["Total Count"]
agegroups["Percentage of Players"] = round(100 * agegroups["Total Count"]/ agegroups["Total Count"].sum(),2)
agegroups
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
      <th>Total Count</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Age Range</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>19</td>
      <td>3.32</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>23</td>
      <td>4.01</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>100</td>
      <td>17.45</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>259</td>
      <td>45.20</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>87</td>
      <td>15.18</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>47</td>
      <td>8.20</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>27</td>
      <td>4.71</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>11</td>
      <td>1.92</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd_file["Age Range"] = pd.cut(pd_file["Age"], bins, labels = group_names)
pd_file.head()
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
      <th>Age Range</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>35-39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
# percentplayers = round(purchcount / players_count,2) * 100

# percentplayers
```

# Purchasing Analysis (Age)


```python
#Purchase Count
#Analyze the data.
#Groupby demographics
demoGroup = pd_file.groupby("Age Range")
#How many rows per bin
print(demoGroup["Age Range"].count())
#Average of each column within GroupBy
demoGroup.mean()
```

    Age Range
    <10       28
    10-14     35
    15-19    133
    20-24    336
    25-29    125
    30-34     64
    35-39     42
    40+       17
    Name: Age Range, dtype: int64
    




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
    <tr>
      <th>Age Range</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>7.535714</td>
      <td>82.321429</td>
      <td>2.980714</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>12.171429</td>
      <td>90.600000</td>
      <td>2.770000</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>16.631579</td>
      <td>94.443609</td>
      <td>2.905414</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>21.875000</td>
      <td>86.038690</td>
      <td>2.913006</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>26.200000</td>
      <td>93.832000</td>
      <td>2.962640</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>31.609375</td>
      <td>101.453125</td>
      <td>3.082031</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>36.714286</td>
      <td>107.071429</td>
      <td>2.842857</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>40.588235</td>
      <td>90.823529</td>
      <td>3.161765</td>
    </tr>
  </tbody>
</table>
</div>




```python
purchcount = demoGroup["Age Range"].count()
purchcount
```




    Age Range
    <10       28
    10-14     35
    15-19    133
    20-24    336
    25-29    125
    30-34     64
    35-39     42
    40+       17
    Name: Age Range, dtype: int64




```python
#Groupby demographics
#demoGroup = pd_file.groupby("Age Range")
#How many rows per bin
agegroupprice = round(demoGroup["Price"].mean(),2)
agegroupprice
```




    Age Range
    <10      2.98
    10-14    2.77
    15-19    2.91
    20-24    2.91
    25-29    2.96
    30-34    3.08
    35-39    2.84
    40+      3.16
    Name: Price, dtype: float64




```python
purchbyage = round(demoGroup["Price"].sum(),2)
purchbyage
```




    Age Range
    <10       83.46
    10-14     96.95
    15-19    386.42
    20-24    978.77
    25-29    370.33
    30-34    197.25
    35-39    119.40
    40+       53.75
    Name: Price, dtype: float64




```python
normage = round(purchbyage/purchcount,2)
normage
```




    Age Range
    <10      2.98
    10-14    2.77
    15-19    2.91
    20-24    2.91
    25-29    2.96
    30-34    3.08
    35-39    2.84
    40+      3.16
    dtype: float64




```python
#Create a dataframe with Age, Purchase Count, Average Purchase Price, Total Purchase Value and Normalized Totals

ageanalysis = pd.DataFrame({"Purchase Count":purchcount,
                        "Average Purchase Price":agegroupprice,
                         "Total Purchase Value":purchbyage,
                          "Normalized Total": normage} )
ageanalysis
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
      <th>Average Purchase Price</th>
      <th>Normalized Total</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Age Range</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>2.98</td>
      <td>2.98</td>
      <td>28</td>
      <td>83.46</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>2.77</td>
      <td>2.77</td>
      <td>35</td>
      <td>96.95</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>2.91</td>
      <td>2.91</td>
      <td>133</td>
      <td>386.42</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>2.91</td>
      <td>2.91</td>
      <td>336</td>
      <td>978.77</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>2.96</td>
      <td>2.96</td>
      <td>125</td>
      <td>370.33</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>3.08</td>
      <td>3.08</td>
      <td>64</td>
      <td>197.25</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>2.84</td>
      <td>2.84</td>
      <td>42</td>
      <td>119.40</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>3.16</td>
      <td>3.16</td>
      <td>17</td>
      <td>53.75</td>
    </tr>
  </tbody>
</table>
</div>



Top Spenders


```python
#Top 5 spenders by total purchase value
topspender = pd_file.groupby("SN").sum()
topspender = topspender.sort_values('Price').tail()
del topspender["Item ID"]
del topspender["Age"]
topspend = topspender.sort_values('Price').tail()
print(topspend)
```

                 Price
    SN                
    Eoda93       11.58
    Haellysu29   12.73
    Mindimnya67  12.74
    Saedue76     13.56
    Undirrala66  17.06
    


```python
#Top 5 spenders total purchases
numpurch = pd.DataFrame(pd_file.groupby("SN").count())

#Top 5 spenders total purchase value
topspender = pd.DataFrame(pd_file.groupby("SN").sum())

#Sort the total purchase price. The default to sort_values is ascending. If I put , ascending=False would be descending.
topspender = topspender.sort_values(by=["Price"])


topspender["Purchase Count"] = numpurch["Item ID"]
topspender["Average Purchase Price"] = round(topspender["Price"]/topspender["Purchase Count"],2).map("${:,.2f}".format)
topspender["Total Purchase Value"] = topspender["Price"].map("${:,.2f}".format)

#I could have done topspender.head() if I sorted descending. 
topspender.tail()
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
      <th>Item ID</th>
      <th>Price</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Eoda93</th>
      <td>66</td>
      <td>284</td>
      <td>11.58</td>
      <td>3</td>
      <td>$3.86</td>
      <td>$11.58</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>63</td>
      <td>353</td>
      <td>12.73</td>
      <td>3</td>
      <td>$4.24</td>
      <td>$12.73</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>156</td>
      <td>609</td>
      <td>12.74</td>
      <td>4</td>
      <td>$3.18</td>
      <td>$12.74</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>100</td>
      <td>233</td>
      <td>13.56</td>
      <td>4</td>
      <td>$3.39</td>
      <td>$13.56</td>
    </tr>
    <tr>
      <th>Undirrala66</th>
      <td>145</td>
      <td>472</td>
      <td>17.06</td>
      <td>5</td>
      <td>$3.41</td>
      <td>$17.06</td>
    </tr>
  </tbody>
</table>
</div>




```python
#pd_file.head()
pd_file = pd_file.drop(labels = ["Age Range"],axis = 1)
pd_file.head()
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
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
topspendpurchcount = pd.DataFrame(pd_file.groupby(["Item ID", "Item Name"]).count())
topspendpurchcount.head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <th>Splinter</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <th>Crucifer</th>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <th>Verdict</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <th>Phantomlight</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <th>Bloodlord's Fetish</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



# Most Popular Items


```python
#Most Popular Items
topspendpurchcount = pd.DataFrame(pd_file.groupby(["Item ID", "Item Name"]).count())
#print(topspendpurchcount)

#Top 5 spenders total purchase value
topitemvalue = pd.DataFrame(pd_file.groupby(["Item ID","Item Name"]).sum()["Price"])
#topitemvalue

#Renaming SN to Purchase Count as it will show how many times the item was purchased. (A person purchases an item.)
topspendpurchcount["Purchase Count"] = topspendpurchcount["SN"]

#Item Price is the sum of prices paid per item divided by the total number of people who bought it.
topspendpurchcount["Item Price"] = round(topitemvalue["Price"]/topspendpurchcount["SN"],2)

#Total Purchase Value is the sum of prices. This is in the topvalueitem dataframe.
topspendpurchcount["Total Purchase Value"] = topitemvalue["Price"]

#The most popular items by purchase count would require us to sort by purchase count descending (highest to lowest).
topspendpurchcount = topspendpurchcount.sort_values(by = ["Purchase Count","Total Purchase Value"],ascending = False)
#topspendpurchcount = topspendpurchcount.sort_values(by = ["Purchase Count"],ascending = False)

#Deleting columns that are not necessary to output. This was not deleted from our original data source, pd_file.
topspendpurchcount = topspendpurchcount.drop(labels = ["Age","Gender","Price","SN"],axis = 1)

##Format the columns for currency as they are monetary values.
topspendpurchcount["Item Price"] = topspendpurchcount["Item Price"].map("${:,.2f}".format)
topspendpurchcount["Total Purchase Value"] = topspendpurchcount["Total Purchase Value"].map("${:,.2f}".format)

#Top 5 Popular Items
topspendpurchcount.head(5)

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
      <th>39</th>
      <th>Betrayal, Whisper of Grieving Widows</th>
      <td>11</td>
      <td>$2.35</td>
      <td>$25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <th>Arcane Gem</th>
      <td>11</td>
      <td>$2.23</td>
      <td>$24.53</td>
    </tr>
    <tr>
      <th>34</th>
      <th>Retribution Axe</th>
      <td>9</td>
      <td>$4.14</td>
      <td>$37.26</td>
    </tr>
    <tr>
      <th>31</th>
      <th>Trickster</th>
      <td>9</td>
      <td>$2.07</td>
      <td>$18.63</td>
    </tr>
    <tr>
      <th>13</th>
      <th>Serenity</th>
      <td>9</td>
      <td>$1.49</td>
      <td>$13.41</td>
    </tr>
  </tbody>
</table>
</div>



Most Profitable Items


```python
#Most Profitable Items
topspendpurchcount = pd.DataFrame(pd_file.groupby(["Item ID", "Item Name"]).count())
#print(topspendpurchcount)

#Top 5 spenders total purchase value
topitemvalue = pd.DataFrame(pd_file.groupby(["Item ID","Item Name"]).sum()["Price"])
#topitemvalue

#Renaming SN to Purchase Count as it will show how many times the item was purchased. (A person purchases an item.)
topspendpurchcount["Purchase Count"] = topspendpurchcount["SN"]

#Item Price is the sum of prices paid per item divided by the total number of people who bought it.
topspendpurchcount["Item Price"] = round(topitemvalue["Price"]/topspendpurchcount["SN"],2)

#Total Purchase Value is the sum of prices. This is in the topvalueitem dataframe.
topspendpurchcount["Total Purchase Value"] = topitemvalue["Price"]

#The most popular items by purchase count would require us to sort by purchase count descending (highest to lowest).
topspendpurchcount = topspendpurchcount.sort_values(by = ["Total Purchase Value", "Purchase Count"],ascending = False)
#topspendpurchcount = topspendpurchcount.sort_values(by = ["Purchase Count"],ascending = False)

#Deleting columns that are not necessary to output. This was not deleted from our original data source, pd_file.
topspendpurchcount = topspendpurchcount.drop(labels = ["Age","Gender","Price","SN"],axis = 1)

##Format the columns for currency as they are monetary values.
topspendpurchcount["Item Price"] = topspendpurchcount["Item Price"].map("${:,.2f}".format)
topspendpurchcount["Total Purchase Value"] = topspendpurchcount["Total Purchase Value"].map("${:,.2f}".format)

#Top 5 Popular Items
topspendpurchcount.head(5)
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
      <th>34</th>
      <th>Retribution Axe</th>
      <td>9</td>
      <td>$4.14</td>
      <td>$37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <th>Spectral Diamond Doomblade</th>
      <td>7</td>
      <td>$4.25</td>
      <td>$29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <th>Orenmir</th>
      <td>6</td>
      <td>$4.95</td>
      <td>$29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>6</td>
      <td>$4.87</td>
      <td>$29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <th>Splitter, Foe Of Subtlety</th>
      <td>8</td>
      <td>$3.61</td>
      <td>$28.88</td>
    </tr>
  </tbody>
</table>
</div>




```python
most_prof_total = pd.DataFrame(pd_file.groupby(['Item ID','Item Name']).count())
most_prof_total.head()
most_prof_total = most_prof_total.groupby(["Item ID","Item Name"]).sum()["Price"]
most_prof_total.head()
```




    Item ID  Item Name         
    0        Splinter              1
    1        Crucifer              4
    2        Verdict               1
    3        Phantomlight          1
    4        Bloodlord's Fetish    1
    Name: Price, dtype: int64




```python
 #Purchase Count
topspendpurchcount = pd_file.groupby("SN").count()
topspendpurchcount = topspendpurchcount.drop(["Age","Gender","Item Name","Price"], axis = 1)
spendpurch = topspendpurchcount.sort_values("Item ID").tail()
spendpurch = spendpurch.rename(columns = {'Item ID': 'Purchase Count'})
print(spendpurch)
```

                 Purchase Count
    SN                         
    Sondastan54               4
    Qarwen67                  4
    Mindimnya67               4
    Hailaphos89               4
    Undirrala66               5
    


```python
#Dataframe by age
#Gender Purchase Analysis
age_df = pd_file.groupby(["Age"])
#age_df.head()
```


```python
#Purchase Count
agepurcount = pd_file["Age"].value_counts()
agepurcount.head()
```




    20    98
    24    70
    22    68
    25    67
    23    57
    Name: Age, dtype: int64




```python
#Total Purchase Value
purchbyage = age_df["Price"].sum()
#purchbyage
```
