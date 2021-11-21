# Cleaning Data
Here I will demonstrate 2 ways I have cleaned data in NESC 3505 assignments 
## #1 Removing Outliers

### Determining the length of the lists
Assignment 3 used two lists. One containing the reaction times (rt) and another containing whether or not the participant made an error (err). Early on in the assignment I print the lengths of both the lists to use as a reference to ensure undesired values have been deleted.


```python
len(rt)
```




    24




```python
print(len(err))
```

    24


The length of the lists are the same as earlier in the assignment I corrected missing values in the err list. Since both lists contain a piece of data from each participant, they are the same size.

### Finding the position of the slowest reaction time
The slowest reaction time is the greatest reaction time value.


```python
slowestRT = rt.index(max(rt))
```

### Remove the slowest reaction time from both lists


```python
rt.pop(slowestRT)
err.pop(slowestRT)
```

### Presenting the updated stats


```python
print(max(rt))
print("rt length:", len(rt) , "err length:" , len(err))
```

    0.844916827
    rt length: 23 err length: 23


I printed the new slowest reaction time and the lengths of both lists to ensure the targeted reaction time was removed

## #2 Removing unknown (NaN) values
### Count the NaN values 
Here I am using .isna() to determine where there are NaN values and .sum() to count how many values are missing from each column 


```python
df.isna().sum()
```




    index                  0
    id                     0
    year                   0
    month                  0
    day                    0
    hour                   0
    minute                 0
    gender                 0
    age                    0
    handedness             0
    wait                   0
    block                  0
    trial                  0
    target_location        0
    target                 0
    flankers               0
    rt                     2
    response               2
    error                  2
    pre_target_response    0
    ITI_response           0
    target_on_error        0
    dtype: int64



As you can see, there are 2 NaN values in the rt, response, and error columns

### Delete trials with missing values
Below I am using .dropna() to delete all rows that have a missing value (NaN)


```python
df.dropna()
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
      <th>index</th>
      <th>id</th>
      <th>year</th>
      <th>month</th>
      <th>day</th>
      <th>hour</th>
      <th>minute</th>
      <th>gender</th>
      <th>age</th>
      <th>handedness</th>
      <th>wait</th>
      <th>block</th>
      <th>trial</th>
      <th>target_location</th>
      <th>target</th>
      <th>flankers</th>
      <th>rt</th>
      <th>response</th>
      <th>error</th>
      <th>pre_target_response</th>
      <th>ITI_response</th>
      <th>target_on_error</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>2</td>
      <td>2015</td>
      <td>5</td>
      <td>25</td>
      <td>14</td>
      <td>36</td>
      <td>f</td>
      <td>21</td>
      <td>r</td>
      <td>12.269</td>
      <td>practice</td>
      <td>1</td>
      <td>left</td>
      <td>black</td>
      <td>incongruent</td>
      <td>0.722</td>
      <td>black</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.024</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2</td>
      <td>2015</td>
      <td>5</td>
      <td>25</td>
      <td>14</td>
      <td>36</td>
      <td>f</td>
      <td>21</td>
      <td>r</td>
      <td>12.269</td>
      <td>practice</td>
      <td>2</td>
      <td>right</td>
      <td>black</td>
      <td>incongruent</td>
      <td>0.472</td>
      <td>black</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.024</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>2</td>
      <td>2015</td>
      <td>5</td>
      <td>25</td>
      <td>14</td>
      <td>36</td>
      <td>f</td>
      <td>21</td>
      <td>r</td>
      <td>12.269</td>
      <td>practice</td>
      <td>3</td>
      <td>up</td>
      <td>white</td>
      <td>incongruent</td>
      <td>0.412</td>
      <td>white</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.024</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>2</td>
      <td>2015</td>
      <td>5</td>
      <td>25</td>
      <td>14</td>
      <td>36</td>
      <td>f</td>
      <td>21</td>
      <td>r</td>
      <td>12.269</td>
      <td>practice</td>
      <td>4</td>
      <td>up</td>
      <td>black</td>
      <td>congruent</td>
      <td>0.560</td>
      <td>black</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.024</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>2</td>
      <td>2015</td>
      <td>5</td>
      <td>25</td>
      <td>14</td>
      <td>36</td>
      <td>f</td>
      <td>21</td>
      <td>r</td>
      <td>12.269</td>
      <td>practice</td>
      <td>5</td>
      <td>down</td>
      <td>black</td>
      <td>congruent</td>
      <td>0.496</td>
      <td>black</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.024</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>571</th>
      <td>187</td>
      <td>3</td>
      <td>2015</td>
      <td>5</td>
      <td>28</td>
      <td>14</td>
      <td>9</td>
      <td>f</td>
      <td>50</td>
      <td>r</td>
      <td>6.539</td>
      <td>5</td>
      <td>28</td>
      <td>left</td>
      <td>white</td>
      <td>congruent</td>
      <td>0.462</td>
      <td>white</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.023</td>
    </tr>
    <tr>
      <th>572</th>
      <td>188</td>
      <td>3</td>
      <td>2015</td>
      <td>5</td>
      <td>28</td>
      <td>14</td>
      <td>9</td>
      <td>f</td>
      <td>50</td>
      <td>r</td>
      <td>6.539</td>
      <td>5</td>
      <td>29</td>
      <td>right</td>
      <td>white</td>
      <td>congruent</td>
      <td>0.353</td>
      <td>white</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.024</td>
    </tr>
    <tr>
      <th>573</th>
      <td>189</td>
      <td>3</td>
      <td>2015</td>
      <td>5</td>
      <td>28</td>
      <td>14</td>
      <td>9</td>
      <td>f</td>
      <td>50</td>
      <td>r</td>
      <td>6.539</td>
      <td>5</td>
      <td>30</td>
      <td>up</td>
      <td>black</td>
      <td>incongruent</td>
      <td>0.380</td>
      <td>white</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>0.024</td>
    </tr>
    <tr>
      <th>574</th>
      <td>190</td>
      <td>3</td>
      <td>2015</td>
      <td>5</td>
      <td>28</td>
      <td>14</td>
      <td>9</td>
      <td>f</td>
      <td>50</td>
      <td>r</td>
      <td>6.539</td>
      <td>5</td>
      <td>31</td>
      <td>left</td>
      <td>white</td>
      <td>neutral</td>
      <td>0.517</td>
      <td>white</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.023</td>
    </tr>
    <tr>
      <th>575</th>
      <td>191</td>
      <td>3</td>
      <td>2015</td>
      <td>5</td>
      <td>28</td>
      <td>14</td>
      <td>9</td>
      <td>f</td>
      <td>50</td>
      <td>r</td>
      <td>6.539</td>
      <td>5</td>
      <td>32</td>
      <td>right</td>
      <td>black</td>
      <td>neutral</td>
      <td>0.444</td>
      <td>black</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.024</td>
    </tr>
  </tbody>
</table>
<p>574 rows × 22 columns</p>
</div>



### Check to ensure rows with missing values have been deleted 


```python
df.isna().sum()
```




    index                  0
    id                     0
    year                   0
    month                  0
    day                    0
    hour                   0
    minute                 0
    gender                 0
    age                    0
    handedness             0
    wait                   0
    block                  0
    trial                  0
    target_location        0
    target                 0
    flankers               0
    rt                     0
    response               0
    error                  0
    pre_target_response    0
    ITI_response           0
    target_on_error        0
    rt_ms                  0
    dtype: int64



As you can see the rt, response, and error columns no longer have rows with missing values. 


```python

```
