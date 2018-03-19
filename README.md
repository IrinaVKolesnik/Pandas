

```python
#imports
import pandas as pd
import numpy as np
import json
```


```python
# read the json file  // THERE IS ONLY ONE DATA SET FOR THIS PROBLEM
with open('purchase_data.json') as file:
    j_data = json.load(file)

```


```python
# to see the dataframe keys
head = j_data[0].keys()
print(head)    
df = pd.DataFrame(j_data)
```

    dict_keys(['SN', 'Age', 'Gender', 'Item ID', 'Item Name', 'Price'])
    


```python
# FINAL REPORT
print("_____________ F I N A L    R E P O R T ________________")
```

    _____________ F I N A L    R E P O R T ________________
    


```python
#Player Count: number of unique players
print("Total Number of Players: ", df["SN"].nunique())
```

    Total Number of Players:  573
    


```python
#Purchasing Analysis (Total)
    
print("Number of Unique Items: ", df["Item Name"].nunique())
print("Average Purchase Price:", round(df["Price"].mean(), 2))
print("Total Number of Purchases: ", df["Item Name"].count())
print("Total Revenue", round(df["Price"].sum(), 2))
```

    Number of Unique Items:  179
    Average Purchase Price: 2.93
    Total Number of Purchases:  780
    Total Revenue 2286.33
    


```python
# Gender Demographics

# Count and Percentage of Male Players
# Count and Percentage of Female Players
# Count and Percentage of Other / Non-Disclosed

df_SN = df[["SN", "Gender"]].drop_duplicates()
genders = df_SN.groupby(['Gender']).count().reset_index().rename(columns={"SN":"Total Count"})
genders["Percentage"] = round(genders["Total Count"] / genders["Total Count"].sum() * 100, 2) 
genders
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Total Count</th>
      <th>Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>100</td>
      <td>17.45</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>465</td>
      <td>81.15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>8</td>
      <td>1.40</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis (Gender):
df_price_gender = df[["Gender", "Price"]]
```


```python
#Purchase Count by gender
genders_pa1 = df_price_gender.groupby(['Gender']).count().reset_index().rename(columns={"Price":"Purchase Count"})
genders_pa1
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Purchase Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>136</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>633</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Average Purchase Price
genders_pa2 = round(df_price_gender.groupby(['Gender']).mean().reset_index().rename(columns={"Price":"Average Purchase Price"}), 2)
genders_pa2
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Average Purchase Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>2.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>2.95</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>3.25</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Total Purchase Value
genders_pa3 = round(df_price_gender.groupby(['Gender']).sum().reset_index().rename(columns={"Price":"Total Purchase Value"}), 2)
genders_pa3
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>382.91</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>1867.68</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>35.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merging df's together
genders_all1 = pd.merge(genders_pa1, genders_pa2, on="Gender")
genders_all2 = pd.merge(genders_all1, genders_pa3, on="Gender")
genders_all = pd.merge(genders_all2, genders, on="Gender")
genders_all
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Total Count</th>
      <th>Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>136</td>
      <td>2.82</td>
      <td>382.91</td>
      <td>100</td>
      <td>17.45</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>633</td>
      <td>2.95</td>
      <td>1867.68</td>
      <td>465</td>
      <td>81.15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>11</td>
      <td>3.25</td>
      <td>35.74</td>
      <td>8</td>
      <td>1.40</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis (Gender): FINAL RESULTS
genders_all["Normalized Total"] = round(genders_all["Total Purchase Value"] / genders_all["Total Count"], 2)
genders_all
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Total Count</th>
      <th>Percentage</th>
      <th>Normalized Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>136</td>
      <td>2.82</td>
      <td>382.91</td>
      <td>100</td>
      <td>17.45</td>
      <td>3.83</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>633</td>
      <td>2.95</td>
      <td>1867.68</td>
      <td>465</td>
      <td>81.15</td>
      <td>4.02</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>11</td>
      <td>3.25</td>
      <td>35.74</td>
      <td>8</td>
      <td>1.40</td>
      <td>4.47</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Age Demographics

# The below each broken into bins of 4 years (i.e. <10, 10-14, 15-19, etc.)
# Create the bins in which Data will be held
my_bins = [0,10,14,19,24,29,34,39,44,49]
```


```python
# Create the names for the four bins
my_labels=["0-9","10-14","15-19","20-24","25-29","30-34","35-39","40-44","45-49"]
```


```python
#  place the Ages into bins
#df_price_age = df[["Age", "Price"]]
#df_price_age
df["Age Groups"]=pd.cut(df["Age"], bins=my_bins, labels=my_labels)
df.head(10)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <th>Age Groups</th>
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
    <tr>
      <th>5</th>
      <td>20</td>
      <td>Male</td>
      <td>10</td>
      <td>Sleepwalker</td>
      <td>1.73</td>
      <td>Tanimnya91</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>6</th>
      <td>20</td>
      <td>Male</td>
      <td>153</td>
      <td>Mercenary Sabre</td>
      <td>4.57</td>
      <td>Undjaskla97</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>7</th>
      <td>29</td>
      <td>Female</td>
      <td>169</td>
      <td>Interrogator, Blood Blade of the Queen</td>
      <td>3.32</td>
      <td>Iathenudil29</td>
      <td>25-29</td>
    </tr>
    <tr>
      <th>8</th>
      <td>25</td>
      <td>Male</td>
      <td>118</td>
      <td>Ghost Reaver, Longsword of Magic</td>
      <td>2.77</td>
      <td>Sondenasta63</td>
      <td>25-29</td>
    </tr>
    <tr>
      <th>9</th>
      <td>31</td>
      <td>Male</td>
      <td>99</td>
      <td>Expiration, Warscythe Of Lost Worlds</td>
      <td>4.53</td>
      <td>Hilaerin92</td>
      <td>30-34</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_age = df[["Age Groups", "Price"]]
df_age.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Groups</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>35-39</td>
      <td>3.37</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20-24</td>
      <td>2.32</td>
    </tr>
    <tr>
      <th>2</th>
      <td>30-34</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>1.36</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20-24</td>
      <td>1.27</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Purchase Count
age_pa1 = df_age.groupby(['Age Groups']).count().reset_index().rename(columns={"Price":"Purchase Count"})
age_pa1
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Groups</th>
      <th>Purchase Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0-9</td>
      <td>32</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>133</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>336</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>125</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>64</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>42</td>
    </tr>
    <tr>
      <th>7</th>
      <td>40-44</td>
      <td>16</td>
    </tr>
    <tr>
      <th>8</th>
      <td>45-49</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Average Purchase Price
age_pa2 = round(df_age.groupby(['Age Groups']).mean().reset_index().rename(columns={"Price":"Average Purchase Price"}), 2)
age_pa2
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Groups</th>
      <th>Average Purchase Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0-9</td>
      <td>3.02</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>2.70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>2.91</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>2.91</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>2.96</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>3.08</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>2.84</td>
    </tr>
    <tr>
      <th>7</th>
      <td>40-44</td>
      <td>3.19</td>
    </tr>
    <tr>
      <th>8</th>
      <td>45-49</td>
      <td>2.72</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Total Purchase Value
age_pa3 = round(df_age.groupby(['Age Groups']).sum().reset_index().rename(columns={"Price":"Total Purchase Value"}), 2)
age_pa3
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Groups</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0-9</td>
      <td>96.62</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>83.79</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>386.42</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>978.77</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>370.33</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>197.25</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>119.40</td>
    </tr>
    <tr>
      <th>7</th>
      <td>40-44</td>
      <td>51.03</td>
    </tr>
    <tr>
      <th>8</th>
      <td>45-49</td>
      <td>2.72</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_SN_age = df[["SN", "Age Groups"]].drop_duplicates()
ages_by_SN = df_SN_age.groupby(['Age Groups']).count().reset_index().rename(columns={"SN":"Total Count"})
ages_by_SN
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Groups</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0-9</td>
      <td>22</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>100</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>259</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>87</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>47</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>27</td>
    </tr>
    <tr>
      <th>7</th>
      <td>40-44</td>
      <td>10</td>
    </tr>
    <tr>
      <th>8</th>
      <td>45-49</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merging dfs
age_all1 = pd.merge(age_pa1, age_pa2, on="Age Groups")
age_all2 = pd.merge(age_all1, age_pa3, on="Age Groups")
age_all = pd.merge(age_all2, ages_by_SN, on="Age Groups")
age_all
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Groups</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0-9</td>
      <td>32</td>
      <td>3.02</td>
      <td>96.62</td>
      <td>22</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>31</td>
      <td>2.70</td>
      <td>83.79</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>133</td>
      <td>2.91</td>
      <td>386.42</td>
      <td>100</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>336</td>
      <td>2.91</td>
      <td>978.77</td>
      <td>259</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>125</td>
      <td>2.96</td>
      <td>370.33</td>
      <td>87</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>64</td>
      <td>3.08</td>
      <td>197.25</td>
      <td>47</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>42</td>
      <td>2.84</td>
      <td>119.40</td>
      <td>27</td>
    </tr>
    <tr>
      <th>7</th>
      <td>40-44</td>
      <td>16</td>
      <td>3.19</td>
      <td>51.03</td>
      <td>10</td>
    </tr>
    <tr>
      <th>8</th>
      <td>45-49</td>
      <td>1</td>
      <td>2.72</td>
      <td>2.72</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Age Demographics - FINAL RESULTS
# +Normalized Totals
age_all["Normalized Total"] = round(age_all["Total Purchase Value"] / age_all["Total Count"], 2)
age_all
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Groups</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Total Count</th>
      <th>Normalized Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0-9</td>
      <td>32</td>
      <td>3.02</td>
      <td>96.62</td>
      <td>22</td>
      <td>4.39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>31</td>
      <td>2.70</td>
      <td>83.79</td>
      <td>20</td>
      <td>4.19</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>133</td>
      <td>2.91</td>
      <td>386.42</td>
      <td>100</td>
      <td>3.86</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>336</td>
      <td>2.91</td>
      <td>978.77</td>
      <td>259</td>
      <td>3.78</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>125</td>
      <td>2.96</td>
      <td>370.33</td>
      <td>87</td>
      <td>4.26</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>64</td>
      <td>3.08</td>
      <td>197.25</td>
      <td>47</td>
      <td>4.20</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>42</td>
      <td>2.84</td>
      <td>119.40</td>
      <td>27</td>
      <td>4.42</td>
    </tr>
    <tr>
      <th>7</th>
      <td>40-44</td>
      <td>16</td>
      <td>3.19</td>
      <td>51.03</td>
      <td>10</td>
      <td>5.10</td>
    </tr>
    <tr>
      <th>8</th>
      <td>45-49</td>
      <td>1</td>
      <td>2.72</td>
      <td>2.72</td>
      <td>1</td>
      <td>2.72</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Top Spenders:

#Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
#"SN", "Purchase Count", "Average Purchase Price", "Total Purchase Value"

df_spenders = pd.DataFrame()

df_by_sn = df.groupby("SN")
for name, group in df_by_sn:
    #print (group)
    cnt = group["Price"].count()
    ave = group["Price"].mean()
    tot = group["Price"].sum()
    df_spenders = df_spenders.append([{"SN":name, "Purchase Count":cnt, "Average Purchase Price": ave, "Total Purchase Value":tot}])
    
my_spenders = df_spenders[["SN", "Purchase Count", "Average Purchase Price", "Total Purchase Value"]]
my_spenders = my_spenders.rename(columns={"SN":"Top Spenders"})
my_spenders.sort_values("Total Purchase Value", ascending=False).head(5) 
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Top Spenders</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Undirrala66</td>
      <td>5</td>
      <td>3.412000</td>
      <td>17.06</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Saedue76</td>
      <td>4</td>
      <td>3.390000</td>
      <td>13.56</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Mindimnya67</td>
      <td>4</td>
      <td>3.185000</td>
      <td>12.74</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Haellysu29</td>
      <td>3</td>
      <td>4.243333</td>
      <td>12.73</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Eoda93</td>
      <td>3</td>
      <td>3.860000</td>
      <td>11.58</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Identify the 5 most popular items by purchase count, then list (in a table):
#"Item ID", "Item Name", "Purchase Count", "Item Price", "Total Purchase Value"
df_pop_items = pd.DataFrame()

df_by_item = df.groupby("Item Name")
for name, group in df_by_item:
    #print (group)
    cnt = group["Price"].count()
    ave = group["Price"].mean()
    tot = group["Price"].sum()
    id = group["Item ID"].min()
    df_pop_items = df_pop_items.append([{"Item ID":id, "Item Name":name, "Purchase Count":cnt, "Item Price": ave, "Total Purchase Value":tot}])

my_pop_items = df_pop_items[["Item Name", "Item ID", "Purchase Count", "Item Price", "Total Purchase Value"]]
my_pop_items = my_pop_items.rename(columns={"Item Name":"Most Popular Items"})    
my_pop_items.sort_values("Purchase Count", ascending=False).head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Most Popular Items</th>
      <th>Item ID</th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Final Critic</td>
      <td>92</td>
      <td>14</td>
      <td>2.757143</td>
      <td>38.60</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Arcane Gem</td>
      <td>84</td>
      <td>11</td>
      <td>2.230000</td>
      <td>24.53</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Betrayal, Whisper of Grieving Widows</td>
      <td>39</td>
      <td>11</td>
      <td>2.350000</td>
      <td>25.85</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Stormcaller</td>
      <td>30</td>
      <td>10</td>
      <td>3.465000</td>
      <td>34.65</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Woeful Adamantite Claymore</td>
      <td>175</td>
      <td>9</td>
      <td>1.240000</td>
      <td>11.16</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Most Profitable Items:

#Identify the 5 most profitable items by total purchase value, then list (in a table):
#"Item ID", "Item Name", "Purchase Count", "Item Price", "Total Purchase Value"

df_prof_items = pd.DataFrame()

df_by_item_prof = df.groupby("Item Name")
for name, group in df_by_item_prof:
    #print (group)
    cnt = group["Price"].count()
    ave = group["Price"].mean()
    tot = group["Price"].sum()
    id = group["Item ID"].min()
    df_prof_items = df_prof_items.append([{"Item ID":id, "Item Name":name, "Purchase Count":cnt, "Item Price": ave, "Total Purchase Value":tot}])

my_prof_items = df_prof_items[["Item Name", "Item ID", "Purchase Count", "Item Price", "Total Purchase Value"]]
my_prof_items = my_prof_items.rename(columns={"Item Name":"Most Profitable Items"})    
my_prof_items.sort_values("Total Purchase Value", ascending=False).head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Most Profitable Items</th>
      <th>Item ID</th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Final Critic</td>
      <td>92</td>
      <td>14</td>
      <td>2.757143</td>
      <td>38.60</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Retribution Axe</td>
      <td>34</td>
      <td>9</td>
      <td>4.140000</td>
      <td>37.26</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Stormcaller</td>
      <td>30</td>
      <td>10</td>
      <td>3.465000</td>
      <td>34.65</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Spectral Diamond Doomblade</td>
      <td>115</td>
      <td>7</td>
      <td>4.250000</td>
      <td>29.75</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Orenmir</td>
      <td>32</td>
      <td>6</td>
      <td>4.950000</td>
      <td>29.70</td>
    </tr>
  </tbody>
</table>
</div>




```python
# I DIDN'T SEE THE SECOND DATA-SET FOR THE 'HEROES OF PYMOLI
```


```python
#http://ucb.bootcampcontent.com/UCB-Coding-Bootcamp/UCBER201802DATA3-Class-Repository-DATA/tree/master/02-Homework/04-Numpy-Pandas/Instructions/HeroesOfPymoli
```
