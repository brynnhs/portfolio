##

# Reading data from files

## Import Pandas
The following lines of code from assignment 3 imports the Pandas library. Pandas contains functions needed to read a csv file


```python
import pandas as pd
```

## Reading the file into a pandas DataFrame
Input the data from subject 1 into a DataFrame using the following line of code


```python
df = pd.read_csv('s01/s01.txt', sep='\t')
```

## Displaying the DataFrame
Subject 1's data is now held in the DataFrame df. A portion of df is shown below. 


```python
df.tail(5)
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
      <th>187</th>
      <td>1</td>
      <td>2015</td>
      <td>5</td>
      <td>22</td>
      <td>11</td>
      <td>30</td>
      <td>m</td>
      <td>25</td>
      <td>r</td>
      <td>1.627</td>
      <td>5</td>
      <td>28</td>
      <td>left</td>
      <td>white</td>
      <td>congruent</td>
      <td>0.349</td>
      <td>white</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.024</td>
    </tr>
    <tr>
      <th>188</th>
      <td>1</td>
      <td>2015</td>
      <td>5</td>
      <td>22</td>
      <td>11</td>
      <td>30</td>
      <td>m</td>
      <td>25</td>
      <td>r</td>
      <td>1.627</td>
      <td>5</td>
      <td>29</td>
      <td>right</td>
      <td>white</td>
      <td>congruent</td>
      <td>0.371</td>
      <td>white</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.023</td>
    </tr>
    <tr>
      <th>189</th>
      <td>1</td>
      <td>2015</td>
      <td>5</td>
      <td>22</td>
      <td>11</td>
      <td>30</td>
      <td>m</td>
      <td>25</td>
      <td>r</td>
      <td>1.627</td>
      <td>5</td>
      <td>30</td>
      <td>up</td>
      <td>black</td>
      <td>incongruent</td>
      <td>0.549</td>
      <td>black</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.023</td>
    </tr>
    <tr>
      <th>190</th>
      <td>1</td>
      <td>2015</td>
      <td>5</td>
      <td>22</td>
      <td>11</td>
      <td>30</td>
      <td>m</td>
      <td>25</td>
      <td>r</td>
      <td>1.627</td>
      <td>5</td>
      <td>31</td>
      <td>left</td>
      <td>white</td>
      <td>neutral</td>
      <td>0.463</td>
      <td>white</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.023</td>
    </tr>
    <tr>
      <th>191</th>
      <td>1</td>
      <td>2015</td>
      <td>5</td>
      <td>22</td>
      <td>11</td>
      <td>30</td>
      <td>m</td>
      <td>25</td>
      <td>r</td>
      <td>1.627</td>
      <td>5</td>
      <td>32</td>
      <td>right</td>
      <td>black</td>
      <td>neutral</td>
      <td>0.430</td>
      <td>black</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.023</td>
    </tr>
  </tbody>
</table>
</div>



The code above shows the last 5 values of df. If we were to just use df.tail(), it would show us the last 10 values of the DataFrame.

# Reading Multiple Files
## Import and use glob


```python
import glob
sub_files = glob.glob('s??/s??.txt')
```

Here, I am importing pythons glob package and using it to list all of subjects .txt files. All subjects have a file starting with s followed by a two digit ID number. I used '??' as the id number to find all of subjects files and their corresponding .txt file. 

## Reading the .txt files
To read each participants file I have used list comprehension to include a for loop within my list. The code will loop through and add each subjects file to a list called sub_data. This produces a list of individual DataFrames; one DataFrame for each subject. To put all of the subjects data into one DataFrame, I used pd.concat() to concatenate all of the participants data files.


```python
sub_data = [pd.read_csv(file, sep='\t') for file in sub_files]
df = pd.concat(sub_data)
```

## The complete DataFrame
Next I used df.reset_index() to ensure all of the trials had unique index numbers and then printed a random sample of 8 values from df


```python
import glob
subFiles = glob.glob('s**/s**.txt')
subData = [pd.read_csv(file, sep='\t') for file in subFiles]
df = pd.concat(subData)
df = df.reset_index()
df.sample(8)
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
      <th>313</th>
      <td>121</td>
      <td>2</td>
      <td>2015</td>
      <td>5</td>
      <td>25</td>
      <td>14</td>
      <td>36</td>
      <td>f</td>
      <td>21</td>
      <td>r</td>
      <td>12.508</td>
      <td>3</td>
      <td>26</td>
      <td>right</td>
      <td>white</td>
      <td>congruent</td>
      <td>0.409</td>
      <td>white</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.024</td>
    </tr>
    <tr>
      <th>365</th>
      <td>173</td>
      <td>2</td>
      <td>2015</td>
      <td>5</td>
      <td>25</td>
      <td>14</td>
      <td>36</td>
      <td>f</td>
      <td>21</td>
      <td>r</td>
      <td>3.096</td>
      <td>5</td>
      <td>14</td>
      <td>left</td>
      <td>black</td>
      <td>neutral</td>
      <td>0.429</td>
      <td>black</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.024</td>
    </tr>
    <tr>
      <th>334</th>
      <td>142</td>
      <td>2</td>
      <td>2015</td>
      <td>5</td>
      <td>25</td>
      <td>14</td>
      <td>36</td>
      <td>f</td>
      <td>21</td>
      <td>r</td>
      <td>2.156</td>
      <td>4</td>
      <td>15</td>
      <td>down</td>
      <td>black</td>
      <td>congruent</td>
      <td>0.460</td>
      <td>black</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.024</td>
    </tr>
    <tr>
      <th>235</th>
      <td>43</td>
      <td>2</td>
      <td>2015</td>
      <td>5</td>
      <td>25</td>
      <td>14</td>
      <td>36</td>
      <td>f</td>
      <td>21</td>
      <td>r</td>
      <td>4.677</td>
      <td>1</td>
      <td>12</td>
      <td>left</td>
      <td>white</td>
      <td>incongruent</td>
      <td>0.451</td>
      <td>black</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>0.024</td>
    </tr>
    <tr>
      <th>525</th>
      <td>141</td>
      <td>1</td>
      <td>2015</td>
      <td>5</td>
      <td>22</td>
      <td>11</td>
      <td>30</td>
      <td>m</td>
      <td>25</td>
      <td>r</td>
      <td>1.599</td>
      <td>4</td>
      <td>14</td>
      <td>down</td>
      <td>white</td>
      <td>neutral</td>
      <td>0.818</td>
      <td>black</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>0.023</td>
    </tr>
    <tr>
      <th>498</th>
      <td>114</td>
      <td>1</td>
      <td>2015</td>
      <td>5</td>
      <td>22</td>
      <td>11</td>
      <td>30</td>
      <td>m</td>
      <td>25</td>
      <td>r</td>
      <td>1.392</td>
      <td>3</td>
      <td>19</td>
      <td>down</td>
      <td>black</td>
      <td>congruent</td>
      <td>0.551</td>
      <td>black</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.023</td>
    </tr>
    <tr>
      <th>409</th>
      <td>25</td>
      <td>1</td>
      <td>2015</td>
      <td>5</td>
      <td>22</td>
      <td>11</td>
      <td>30</td>
      <td>m</td>
      <td>25</td>
      <td>r</td>
      <td>3.240</td>
      <td>practice</td>
      <td>26</td>
      <td>up</td>
      <td>white</td>
      <td>congruent</td>
      <td>0.425</td>
      <td>white</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>0.023</td>
    </tr>
    <tr>
      <th>351</th>
      <td>159</td>
      <td>2</td>
      <td>2015</td>
      <td>5</td>
      <td>25</td>
      <td>14</td>
      <td>36</td>
      <td>f</td>
      <td>21</td>
      <td>r</td>
      <td>2.156</td>
      <td>4</td>
      <td>32</td>
      <td>left</td>
      <td>black</td>
      <td>incongruent</td>
      <td>0.728</td>
      <td>white</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>0.024</td>
    </tr>
  </tbody>
</table>
</div>


