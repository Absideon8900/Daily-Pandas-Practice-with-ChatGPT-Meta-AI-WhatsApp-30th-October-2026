# Daily Pandas Practice with ChatGPT Meta-AI WhatsApp 30th October 2026
<b>New Dataset: Satellite-Based Land Monitoring</b></br>
Imagine you're analyzing environmental conditions across different monitoring sites.</br>
```Python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "site_id": [201, 202, 203, 204, 205, 206, 207, 208, 209, 210],
    "district": [
        "Kolkata", "Howrah", "Cuttack", "Patna", "Kolkata",
        "Guwahati", "Patna", "Howrah", "Cuttack", "Guwahati"
    ],
    "landuse": [
        "Urban", "Agriculture", "Forest", "Urban", "Forest",
        "Agriculture", "Forest", "Urban", "Agriculture", "Forest"
    ],
    "ndvi": [0.24, 0.62, 0.81, 0.31, np.nan,
             0.55, 0.76, 0.28, np.nan, 0.88],
    "rainfall": [320, 180, 240, 410, 290,
                 np.nan, 350, 190, 270, 460],
    "elevation": [12, 45, 120, 55, 18,
                  72, 95, 30, 65, 110]
})

print(df)
```
<b>Challenge 1 - Conditional Filtering</b></br>
Create a new Dataframe named <code>vegetation_df</code> containing sites that satisfy <b>both</b> conditions:</br>
Rules:</br>
<ul>
  <li><code>ndvi</code> is greater than <code>0.60</code></li>
  <li><code>rainfall</code> is greater than or equal to <code>250</code></li>
</ul>


<b>Challenge 2 - Create a new column</b></br>
Let's increase the difficulty slightly</br>
Using the original <code>df</code>, create a new column called <code>vegetation_status</code></br>
Rules:</br>
<ul>
  <li>NDVI is greater than or equal to <code>0.70</code> -> <code>"Dense_Vegatation"</code></li>
  <li>NDVI is below <code>0.70</code> -> <code>"Other Vegetation"</code></li>
  <li>Missing NDVI -> <code>"Unknown"</code></li>
</ul>


<b>Challenge 3 - GroupBy + transform</b></br>
Now let's move up a level using the same dataset.</br>
<b>Task</b>: Create a new column named <code>district_avg_ndvi</code> that contains the average NDVI for each district, while keeping the every original row</br>
Rules:</br>
<ul>
  <li>Calculate the main NDVI for each district</li>
  <li>Missing NDVI values should be ignored when calculating the mean</li>
  <li>The resulting Dataframe must retain all 10 rows</li>
</ul>


<b>Challenge 4 - GroupBy + agg</b></br>
Now let's test a slightly different skill</br>
Create a new Dataframe called <code>district_summary</code> that contains:</br>
<ul>
  <li><code>mean_ndvi</code> - average NDVI for each district</li>
  <li><code>total_rainfall</code> - total rainfall for each district</li>
  <li><code>site_count</code> - number of sites in each district</li>
</ul>
Rules:</br>
<ul>
  <li>Use <code>groupby()</code> and <code>agg()</code></li>
  <li>Keep one row per district</li>
  <li>Missing values should be handled uning Pandas's default aggression behaviour</li>
</ul>


<b>Challenge 5 - Boolean filtering + GroupBy</b><>
Using the same original <code>df</code>, create <code>high_vegetation_sites</code> containing only sites where:</br>
<ul>
  <li><code>ndvi</code> is greater than <code>0.60</code></li>
  <li><code>rainfall</code> is greater than <code>200</code></li>
</ul>
Then calculate the <b>number of qualifying sites in each district.</b>

<b>Challenge 6 - Your next task</b></br>
Create a dataframe called <code>landuse_summary</code> with:</br>
<ul>
  <li><code>landuse</code></li>
  <li><code>mean_ndvi</code></li>
  <li><code>max_rainfall</code></li>
  <li><code>site_count</code></li>
</ul>

# Solution (Script)
```Python
import pandas as pd  
import numpy as np  
  
df = pd.DataFrame({  
    "site_id": [201, 202, 203, 204, 205, 206, 207, 208, 209, 210],  
    "district": [  
        "Kolkata", "Howrah", "Cuttack", "Patna", "Kolkata",  
        "Guwahati", "Patna", "Howrah", "Cuttack", "Guwahati"  
    ],  
    "landuse": [  
        "Urban", "Agriculture", "Forest", "Urban", "Forest",  
        "Agriculture", "Forest", "Urban", "Agriculture", "Forest"  
    ],  
    "ndvi": [0.24, 0.62, 0.81, 0.31, np.nan,  
             0.55, 0.76, 0.28, np.nan, 0.88],  
    "rainfall": [320, 180, 240, 410, 290,  
                 np.nan, 350, 190, 270, 460],  
    "elevation": [12, 45, 120, 55, 18,  
                  72, 95, 30, 65, 110]  
})  
high_vegetation_sites = df[(df["ndvi"]>0.60)&(df["rainfall"]>200)].groupby("district")[["ndvi","rainfall"]].agg("count").reset_index()  
print(high_vegetation_sites)
```
# Solution (Output)
```
PS C:\Users\hp\Downloads\sql_practice(0)> & C:\Users\hp\AppData\Local\Programs\Python\Python313\python.exe "c:/Users/hp/Downloads/sql_practice(0)/test2.py"
   district  ndvi  rainfall
0   Cuttack     1         1
1  Guwahati     1         1
2     Patna     1         1
PS C:\Users\hp\Downloads\sql_practice(0)> 
```
