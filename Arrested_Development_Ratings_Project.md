ARRESTED DEVELOPMENT RATINGS
WHAT ARE THE BEST AND WORST MOMENTS IN ARRESTED DEVELOPMENT

STEP 1: IMPORT THE DATA


```python
# Reading TSV files using pandas
import pandas as pd
# import os


# Assign file name to a variable
ep_file_path = 'title.episode.tsv.gz' # contains IMDB's full repository of episodes
rate_file_path = 'title.ratings.tsv.gz' # contains IMDB's full repository of ratings
akas_file_path = 'title.akas.tsv.gz' # contains IMDB's full repository of generic show info, including name


# Use .read_csv() with args to unzip the tsv.gz for each file 
ep = pd.read_csv(ep_file_path, sep='\t', compression = 'gzip')
rate = pd.read_csv(rate_file_path, sep='\t', compression = 'gzip')
akas = pd.read_csv(akas_file_path, sep='\t', compression = 'gzip')

# print(os.getcwd()) # Check where the working directory is
# # Run this to check whether file is in the correct directory:
# if os.path.exists(file_path):
#     df = pd.read_csv(file_path, sep='\t', compression='gzip')
# else:
#     print("File does not exist.")
```

    /var/folders/n4/lff0x4bd7h137vxw7zpjzwn00000gq/T/ipykernel_51636/2424429200.py:15: DtypeWarning: Columns (7) have mixed types. Specify dtype option on import or set low_memory=False.
      akas = pd.read_csv(akas_file_path, sep='\t', compression = 'gzip')





    (            tconst parentTconst seasonNumber episodeNumber
     0        tt0041951    tt0041038            1             9
     1        tt0042816    tt0989125            1            17
     2        tt0042889    tt0989125           \N            \N
     3        tt0043426    tt0040051            3            42
     4        tt0043631    tt0989125            2            16
     ...            ...          ...          ...           ...
     7658160  tt9916846    tt1289683            3            18
     7658161  tt9916848    tt1289683            3            17
     7658162  tt9916850    tt1289683            3            19
     7658163  tt9916852    tt1289683            3            20
     7658164  tt9916880    tt0985991            4             2
     
     [7658165 rows x 4 columns],
                 tconst  averageRating  numVotes
     0        tt0000001            5.7      1990
     1        tt0000002            5.8       265
     2        tt0000003            6.5      1854
     3        tt0000004            5.5       178
     4        tt0000005            6.2      2640
     ...            ...            ...       ...
     1335970  tt9916730            8.3        10
     1335971  tt9916766            7.0        22
     1335972  tt9916778            7.2        36
     1335973  tt9916840            8.8         6
     1335974  tt9916880            8.2         6
     
     [1335975 rows x 3 columns],
                 titleId  ordering                      title region language  \
     0         tt0000001         1                 Карменсіта     UA       \N   
     1         tt0000001         2                 Carmencita     DE       \N   
     2         tt0000001         3  Carmencita - spanyol tánc     HU       \N   
     3         tt0000001         4                 Καρμενσίτα     GR       \N   
     4         tt0000001         5                 Карменсита     RU       \N   
     ...             ...       ...                        ...    ...      ...   
     36788269  tt9916852         5             Episódio #3.20     PT       pt   
     36788270  tt9916852         6             Episodio #3.20     IT       it   
     36788271  tt9916852         7               एपिसोड #3.20     IN       hi   
     36788272  tt9916856         1                   The Wind     DE       \N   
     36788273  tt9916856         2                   The Wind     \N       \N   
     
                     types     attributes isOriginalTitle  
     0         imdbDisplay             \N               0  
     1                  \N  literal title               0  
     2         imdbDisplay             \N               0  
     3         imdbDisplay             \N               0  
     4         imdbDisplay             \N               0  
     ...               ...            ...             ...  
     36788269           \N             \N               0  
     36788270           \N             \N               0  
     36788271           \N             \N               0  
     36788272  imdbDisplay             \N               0  
     36788273     original             \N               1  
     
     [36788274 rows x 8 columns])



STEP 2: DATA PREP


```python
# Brief look at the structure of the data
display(ep,rate,akas)
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
      <th>tconst</th>
      <th>parentTconst</th>
      <th>seasonNumber</th>
      <th>episodeNumber</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>tt0041951</td>
      <td>tt0041038</td>
      <td>1</td>
      <td>9</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt0042816</td>
      <td>tt0989125</td>
      <td>1</td>
      <td>17</td>
    </tr>
    <tr>
      <th>2</th>
      <td>tt0042889</td>
      <td>tt0989125</td>
      <td>\N</td>
      <td>\N</td>
    </tr>
    <tr>
      <th>3</th>
      <td>tt0043426</td>
      <td>tt0040051</td>
      <td>3</td>
      <td>42</td>
    </tr>
    <tr>
      <th>4</th>
      <td>tt0043631</td>
      <td>tt0989125</td>
      <td>2</td>
      <td>16</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>7658160</th>
      <td>tt9916846</td>
      <td>tt1289683</td>
      <td>3</td>
      <td>18</td>
    </tr>
    <tr>
      <th>7658161</th>
      <td>tt9916848</td>
      <td>tt1289683</td>
      <td>3</td>
      <td>17</td>
    </tr>
    <tr>
      <th>7658162</th>
      <td>tt9916850</td>
      <td>tt1289683</td>
      <td>3</td>
      <td>19</td>
    </tr>
    <tr>
      <th>7658163</th>
      <td>tt9916852</td>
      <td>tt1289683</td>
      <td>3</td>
      <td>20</td>
    </tr>
    <tr>
      <th>7658164</th>
      <td>tt9916880</td>
      <td>tt0985991</td>
      <td>4</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
<p>7658165 rows × 4 columns</p>
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
      <th>tconst</th>
      <th>averageRating</th>
      <th>numVotes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>tt0000001</td>
      <td>5.7</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt0000002</td>
      <td>5.8</td>
      <td>265</td>
    </tr>
    <tr>
      <th>2</th>
      <td>tt0000003</td>
      <td>6.5</td>
      <td>1854</td>
    </tr>
    <tr>
      <th>3</th>
      <td>tt0000004</td>
      <td>5.5</td>
      <td>178</td>
    </tr>
    <tr>
      <th>4</th>
      <td>tt0000005</td>
      <td>6.2</td>
      <td>2640</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1335970</th>
      <td>tt9916730</td>
      <td>8.3</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1335971</th>
      <td>tt9916766</td>
      <td>7.0</td>
      <td>22</td>
    </tr>
    <tr>
      <th>1335972</th>
      <td>tt9916778</td>
      <td>7.2</td>
      <td>36</td>
    </tr>
    <tr>
      <th>1335973</th>
      <td>tt9916840</td>
      <td>8.8</td>
      <td>6</td>
    </tr>
    <tr>
      <th>1335974</th>
      <td>tt9916880</td>
      <td>8.2</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
<p>1335975 rows × 3 columns</p>
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
      <th>titleId</th>
      <th>ordering</th>
      <th>title</th>
      <th>region</th>
      <th>language</th>
      <th>types</th>
      <th>attributes</th>
      <th>isOriginalTitle</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>tt0000001</td>
      <td>1</td>
      <td>Карменсіта</td>
      <td>UA</td>
      <td>\N</td>
      <td>imdbDisplay</td>
      <td>\N</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt0000001</td>
      <td>2</td>
      <td>Carmencita</td>
      <td>DE</td>
      <td>\N</td>
      <td>\N</td>
      <td>literal title</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>tt0000001</td>
      <td>3</td>
      <td>Carmencita - spanyol tánc</td>
      <td>HU</td>
      <td>\N</td>
      <td>imdbDisplay</td>
      <td>\N</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>tt0000001</td>
      <td>4</td>
      <td>Καρμενσίτα</td>
      <td>GR</td>
      <td>\N</td>
      <td>imdbDisplay</td>
      <td>\N</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>tt0000001</td>
      <td>5</td>
      <td>Карменсита</td>
      <td>RU</td>
      <td>\N</td>
      <td>imdbDisplay</td>
      <td>\N</td>
      <td>0</td>
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
    </tr>
    <tr>
      <th>36788269</th>
      <td>tt9916852</td>
      <td>5</td>
      <td>Episódio #3.20</td>
      <td>PT</td>
      <td>pt</td>
      <td>\N</td>
      <td>\N</td>
      <td>0</td>
    </tr>
    <tr>
      <th>36788270</th>
      <td>tt9916852</td>
      <td>6</td>
      <td>Episodio #3.20</td>
      <td>IT</td>
      <td>it</td>
      <td>\N</td>
      <td>\N</td>
      <td>0</td>
    </tr>
    <tr>
      <th>36788271</th>
      <td>tt9916852</td>
      <td>7</td>
      <td>एपिसोड #3.20</td>
      <td>IN</td>
      <td>hi</td>
      <td>\N</td>
      <td>\N</td>
      <td>0</td>
    </tr>
    <tr>
      <th>36788272</th>
      <td>tt9916856</td>
      <td>1</td>
      <td>The Wind</td>
      <td>DE</td>
      <td>\N</td>
      <td>imdbDisplay</td>
      <td>\N</td>
      <td>0</td>
    </tr>
    <tr>
      <th>36788273</th>
      <td>tt9916856</td>
      <td>2</td>
      <td>The Wind</td>
      <td>\N</td>
      <td>\N</td>
      <td>original</td>
      <td>\N</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>36788274 rows × 8 columns</p>
</div>



```python
## Here, we cross-reference the above tables to determine which data we need and which we can drop.
## We see in the akas_df the 'titleId' and 'title' columns which contain the name of the show we are searching 
## for as well as the ID, which we can see shares the structure of the 'tconst' and 'parentTconst' columns in
## ep_df and rate_df. Since both ep_df and rate_df lack a 'title' column, we will need the ID to work with each table.

print(akas.columns) # check the columns list of akas_df
# akas = akas.drop(['ordering','region','language','types','attributes','isOriginalTitle'],axis=1) # Drop columns

a_df = akas.loc[akas['title'] == 'Arrested Development'] # Filter for the title we are interested in
display(a_df) # View updated table
```

    Index(['titleId', 'title'], dtype='object')



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
      <th>titleId</th>
      <th>title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1808155</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808158</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808161</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808162</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808163</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808164</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808165</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808167</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808168</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808170</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808173</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808175</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808178</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808179</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808182</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808184</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808185</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808188</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808189</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808190</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808193</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808195</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808197</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808200</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808205</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1808206</th>
      <td>tt0367279</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1835584</th>
      <td>tt0376489</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1835585</th>
      <td>tt0376489</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>1835586</th>
      <td>tt0376489</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>2510215</th>
      <td>tt0656233</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>2752375</th>
      <td>tt0757519</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>3002908</th>
      <td>tt0858164</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>3125426</th>
      <td>tt0901469</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>3125427</th>
      <td>tt0901469</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>3125428</th>
      <td>tt0901469</td>
      <td>Arrested Development</td>
    </tr>
    <tr>
      <th>5136478</th>
      <td>tt1077038</td>
      <td>Arrested Development</td>
    </tr>
  </tbody>
</table>
</div>



```python
## Filter and sort episode data. In the previous cell, we see that the 'titleId' that we are interested in is 'tt0367279.'
## Given that, we will create a new DataFrame called episodes which we contain the episode data that matches the 
## 'titleId' we found. 

episodes = pd.DataFrame(ep.loc[ep['parentTconst'] == 'tt0367279'])
episodes['episodeNumber'] = episodes['episodeNumber'].astype(int) # String to int conversion for sorting
for ep in episodes['episodeNumber']:
    if ep < 10:
        episodes['episodeNumber'] = ep
episodes['seasonNumber'] = episodes['seasonNumber'].astype(int) # String to int conversion for sorting

# episodes.sort_values(by=['seasonNumber','episodeNumber'], ascending=[True,True], inplace=True) # Sorting
# pd.set_option('display.max_rows', 100) # Improve the viewing of the data
# display(episodes)

## Though in the akas table we see a few different IDs associated with our title, this data is likely 
## outlier data (shares the same name but is not the same show). To confirm, we recall that our show 
## contains 84 episodes. Then we run the code to confirm:
# episodes.shape # Return the size of the DataFrame for verification
```


```python
## Here we will combine the episode data and the rating data to have our full, usable dataset.

eprate = rate.merge(episodes, on='tconst', how='inner') # Create new table with rating + episode data with an inner join
eprate.sort_values(by=['seasonNumber','episodeNumber'], ascending=[True,True], inplace=True) # Sort values by season and episode
display(eprate) # View dataset

## Tests: 
# print(rate_df.loc[rate_df['tconst'] == 'tt0515207']) # Rating of s2e6 should be 9.0
# print(rate_df.loc[rate_df['tconst'] == 'tt0515208']) # Rating of s1e16 should be 8.5
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
      <th>tconst</th>
      <th>averageRating</th>
      <th>numVotes</th>
      <th>parentTconst</th>
      <th>seasonNumber</th>
      <th>episodeNumber</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>29</th>
      <td>tt0515236</td>
      <td>8.1</td>
      <td>4027</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>49</th>
      <td>tt0515256</td>
      <td>8.4</td>
      <td>3546</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>tt0515212</td>
      <td>8.1</td>
      <td>3238</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>3</td>
    </tr>
    <tr>
      <th>16</th>
      <td>tt0515223</td>
      <td>8.3</td>
      <td>3093</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>7</th>
      <td>tt0515214</td>
      <td>8.2</td>
      <td>2955</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>5</td>
    </tr>
    <tr>
      <th>50</th>
      <td>tt0515257</td>
      <td>8.0</td>
      <td>2843</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>6</td>
    </tr>
    <tr>
      <th>14</th>
      <td>tt0515221</td>
      <td>8.1</td>
      <td>2794</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>7</td>
    </tr>
    <tr>
      <th>24</th>
      <td>tt0515231</td>
      <td>8.0</td>
      <td>2726</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>8</td>
    </tr>
    <tr>
      <th>40</th>
      <td>tt0515247</td>
      <td>8.4</td>
      <td>2698</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>9</td>
    </tr>
    <tr>
      <th>28</th>
      <td>tt0515235</td>
      <td>9.1</td>
      <td>3435</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>10</td>
    </tr>
    <tr>
      <th>31</th>
      <td>tt0515238</td>
      <td>8.2</td>
      <td>2689</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>11</td>
    </tr>
    <tr>
      <th>19</th>
      <td>tt0515226</td>
      <td>8.4</td>
      <td>2620</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>tt0515210</td>
      <td>8.4</td>
      <td>2592</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>13</td>
    </tr>
    <tr>
      <th>37</th>
      <td>tt0515244</td>
      <td>8.5</td>
      <td>2696</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>14</td>
    </tr>
    <tr>
      <th>39</th>
      <td>tt0515246</td>
      <td>8.1</td>
      <td>2520</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt0515208</td>
      <td>8.5</td>
      <td>2554</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>16</td>
    </tr>
    <tr>
      <th>15</th>
      <td>tt0515222</td>
      <td>8.7</td>
      <td>2678</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>17</td>
    </tr>
    <tr>
      <th>21</th>
      <td>tt0515228</td>
      <td>8.2</td>
      <td>2435</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>18</td>
    </tr>
    <tr>
      <th>4</th>
      <td>tt0515211</td>
      <td>8.1</td>
      <td>2422</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>19</td>
    </tr>
    <tr>
      <th>51</th>
      <td>tt0515258</td>
      <td>7.9</td>
      <td>2391</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>20</td>
    </tr>
    <tr>
      <th>25</th>
      <td>tt0515232</td>
      <td>8.5</td>
      <td>2463</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>21</td>
    </tr>
    <tr>
      <th>17</th>
      <td>tt0515224</td>
      <td>8.6</td>
      <td>2523</td>
      <td>tt0367279</td>
      <td>1</td>
      <td>22</td>
    </tr>
    <tr>
      <th>46</th>
      <td>tt0515253</td>
      <td>8.7</td>
      <td>2495</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>47</th>
      <td>tt0515254</td>
      <td>8.5</td>
      <td>2443</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>tt0515209</td>
      <td>8.8</td>
      <td>2604</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>12</th>
      <td>tt0515219</td>
      <td>9.0</td>
      <td>2759</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <th>36</th>
      <td>tt0515243</td>
      <td>8.5</td>
      <td>2318</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>5</td>
    </tr>
    <tr>
      <th>0</th>
      <td>tt0515207</td>
      <td>9.0</td>
      <td>2850</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>6</td>
    </tr>
    <tr>
      <th>41</th>
      <td>tt0515248</td>
      <td>8.1</td>
      <td>2225</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>7</td>
    </tr>
    <tr>
      <th>32</th>
      <td>tt0515239</td>
      <td>8.0</td>
      <td>2186</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>8</td>
    </tr>
    <tr>
      <th>6</th>
      <td>tt0515213</td>
      <td>8.0</td>
      <td>2200</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>9</td>
    </tr>
    <tr>
      <th>33</th>
      <td>tt0515240</td>
      <td>8.3</td>
      <td>2333</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>10</td>
    </tr>
    <tr>
      <th>27</th>
      <td>tt0515234</td>
      <td>8.3</td>
      <td>2183</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>11</td>
    </tr>
    <tr>
      <th>13</th>
      <td>tt0515220</td>
      <td>8.7</td>
      <td>2301</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>12</td>
    </tr>
    <tr>
      <th>22</th>
      <td>tt0515229</td>
      <td>8.6</td>
      <td>2329</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>13</td>
    </tr>
    <tr>
      <th>44</th>
      <td>tt0515251</td>
      <td>8.5</td>
      <td>2242</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>14</td>
    </tr>
    <tr>
      <th>48</th>
      <td>tt0515255</td>
      <td>8.6</td>
      <td>2294</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>15</td>
    </tr>
    <tr>
      <th>20</th>
      <td>tt0515227</td>
      <td>9.0</td>
      <td>2635</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>16</td>
    </tr>
    <tr>
      <th>38</th>
      <td>tt0515245</td>
      <td>8.5</td>
      <td>2183</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>17</td>
    </tr>
    <tr>
      <th>34</th>
      <td>tt0515241</td>
      <td>8.9</td>
      <td>2319</td>
      <td>tt0367279</td>
      <td>2</td>
      <td>18</td>
    </tr>
    <tr>
      <th>43</th>
      <td>tt0515250</td>
      <td>8.6</td>
      <td>2236</td>
      <td>tt0367279</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>42</th>
      <td>tt0515249</td>
      <td>8.3</td>
      <td>2209</td>
      <td>tt0367279</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>11</th>
      <td>tt0515218</td>
      <td>8.6</td>
      <td>2231</td>
      <td>tt0367279</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>26</th>
      <td>tt0515233</td>
      <td>8.2</td>
      <td>2188</td>
      <td>tt0367279</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>23</th>
      <td>tt0515230</td>
      <td>8.7</td>
      <td>2378</td>
      <td>tt0367279</td>
      <td>3</td>
      <td>5</td>
    </tr>
    <tr>
      <th>45</th>
      <td>tt0515252</td>
      <td>8.6</td>
      <td>2225</td>
      <td>tt0367279</td>
      <td>3</td>
      <td>6</td>
    </tr>
    <tr>
      <th>30</th>
      <td>tt0515237</td>
      <td>7.9</td>
      <td>2056</td>
      <td>tt0367279</td>
      <td>3</td>
      <td>7</td>
    </tr>
    <tr>
      <th>18</th>
      <td>tt0515225</td>
      <td>8.7</td>
      <td>2281</td>
      <td>tt0367279</td>
      <td>3</td>
      <td>8</td>
    </tr>
    <tr>
      <th>35</th>
      <td>tt0515242</td>
      <td>8.7</td>
      <td>2338</td>
      <td>tt0367279</td>
      <td>3</td>
      <td>9</td>
    </tr>
    <tr>
      <th>9</th>
      <td>tt0515216</td>
      <td>8.5</td>
      <td>2110</td>
      <td>tt0367279</td>
      <td>3</td>
      <td>10</td>
    </tr>
    <tr>
      <th>10</th>
      <td>tt0515217</td>
      <td>8.6</td>
      <td>2158</td>
      <td>tt0367279</td>
      <td>3</td>
      <td>11</td>
    </tr>
    <tr>
      <th>8</th>
      <td>tt0515215</td>
      <td>8.8</td>
      <td>2206</td>
      <td>tt0367279</td>
      <td>3</td>
      <td>12</td>
    </tr>
    <tr>
      <th>52</th>
      <td>tt0757386</td>
      <td>9.2</td>
      <td>2894</td>
      <td>tt0367279</td>
      <td>3</td>
      <td>13</td>
    </tr>
    <tr>
      <th>53</th>
      <td>tt2128813</td>
      <td>7.3</td>
      <td>2325</td>
      <td>tt0367279</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>55</th>
      <td>tt2128815</td>
      <td>6.8</td>
      <td>1916</td>
      <td>tt0367279</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>56</th>
      <td>tt2128816</td>
      <td>6.9</td>
      <td>1805</td>
      <td>tt0367279</td>
      <td>4</td>
      <td>3</td>
    </tr>
    <tr>
      <th>57</th>
      <td>tt2128817</td>
      <td>7.6</td>
      <td>1694</td>
      <td>tt0367279</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>58</th>
      <td>tt2128818</td>
      <td>7.6</td>
      <td>1691</td>
      <td>tt0367279</td>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>59</th>
      <td>tt2128819</td>
      <td>7.1</td>
      <td>1550</td>
      <td>tt0367279</td>
      <td>4</td>
      <td>6</td>
    </tr>
    <tr>
      <th>60</th>
      <td>tt2128820</td>
      <td>8.2</td>
      <td>1743</td>
      <td>tt0367279</td>
      <td>4</td>
      <td>7</td>
    </tr>
    <tr>
      <th>61</th>
      <td>tt2128821</td>
      <td>7.5</td>
      <td>1506</td>
      <td>tt0367279</td>
      <td>4</td>
      <td>8</td>
    </tr>
    <tr>
      <th>62</th>
      <td>tt2128822</td>
      <td>7.6</td>
      <td>1481</td>
      <td>tt0367279</td>
      <td>4</td>
      <td>9</td>
    </tr>
    <tr>
      <th>54</th>
      <td>tt2128814</td>
      <td>7.6</td>
      <td>1474</td>
      <td>tt0367279</td>
      <td>4</td>
      <td>10</td>
    </tr>
    <tr>
      <th>63</th>
      <td>tt2495824</td>
      <td>8.4</td>
      <td>1642</td>
      <td>tt0367279</td>
      <td>4</td>
      <td>11</td>
    </tr>
    <tr>
      <th>65</th>
      <td>tt2604336</td>
      <td>8.1</td>
      <td>1462</td>
      <td>tt0367279</td>
      <td>4</td>
      <td>12</td>
    </tr>
    <tr>
      <th>64</th>
      <td>tt2604334</td>
      <td>8.1</td>
      <td>1477</td>
      <td>tt0367279</td>
      <td>4</td>
      <td>13</td>
    </tr>
    <tr>
      <th>66</th>
      <td>tt2604338</td>
      <td>8.0</td>
      <td>1475</td>
      <td>tt0367279</td>
      <td>4</td>
      <td>14</td>
    </tr>
    <tr>
      <th>67</th>
      <td>tt2826310</td>
      <td>8.1</td>
      <td>1524</td>
      <td>tt0367279</td>
      <td>4</td>
      <td>15</td>
    </tr>
    <tr>
      <th>68</th>
      <td>tt4589902</td>
      <td>7.0</td>
      <td>1222</td>
      <td>tt0367279</td>
      <td>5</td>
      <td>1</td>
    </tr>
    <tr>
      <th>70</th>
      <td>tt4861452</td>
      <td>7.1</td>
      <td>1076</td>
      <td>tt0367279</td>
      <td>5</td>
      <td>2</td>
    </tr>
    <tr>
      <th>71</th>
      <td>tt4861456</td>
      <td>7.3</td>
      <td>1029</td>
      <td>tt0367279</td>
      <td>5</td>
      <td>3</td>
    </tr>
    <tr>
      <th>72</th>
      <td>tt4861458</td>
      <td>7.3</td>
      <td>997</td>
      <td>tt0367279</td>
      <td>5</td>
      <td>4</td>
    </tr>
    <tr>
      <th>73</th>
      <td>tt4861460</td>
      <td>7.2</td>
      <td>978</td>
      <td>tt0367279</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>74</th>
      <td>tt4861462</td>
      <td>7.5</td>
      <td>978</td>
      <td>tt0367279</td>
      <td>5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>75</th>
      <td>tt4861466</td>
      <td>7.4</td>
      <td>963</td>
      <td>tt0367279</td>
      <td>5</td>
      <td>7</td>
    </tr>
    <tr>
      <th>76</th>
      <td>tt4861470</td>
      <td>7.3</td>
      <td>965</td>
      <td>tt0367279</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>77</th>
      <td>tt4861472</td>
      <td>6.9</td>
      <td>818</td>
      <td>tt0367279</td>
      <td>5</td>
      <td>9</td>
    </tr>
    <tr>
      <th>78</th>
      <td>tt4861478</td>
      <td>6.9</td>
      <td>770</td>
      <td>tt0367279</td>
      <td>5</td>
      <td>10</td>
    </tr>
    <tr>
      <th>79</th>
      <td>tt4861482</td>
      <td>6.7</td>
      <td>739</td>
      <td>tt0367279</td>
      <td>5</td>
      <td>11</td>
    </tr>
    <tr>
      <th>81</th>
      <td>tt4861486</td>
      <td>7.4</td>
      <td>753</td>
      <td>tt0367279</td>
      <td>5</td>
      <td>12</td>
    </tr>
    <tr>
      <th>80</th>
      <td>tt4861484</td>
      <td>6.8</td>
      <td>741</td>
      <td>tt0367279</td>
      <td>5</td>
      <td>13</td>
    </tr>
    <tr>
      <th>82</th>
      <td>tt4861490</td>
      <td>6.6</td>
      <td>738</td>
      <td>tt0367279</td>
      <td>5</td>
      <td>14</td>
    </tr>
    <tr>
      <th>83</th>
      <td>tt4861494</td>
      <td>7.0</td>
      <td>733</td>
      <td>tt0367279</td>
      <td>5</td>
      <td>15</td>
    </tr>
    <tr>
      <th>69</th>
      <td>tt4589904</td>
      <td>7.7</td>
      <td>927</td>
      <td>tt0367279</td>
      <td>5</td>
      <td>16</td>
    </tr>
  </tbody>
</table>
</div>



```python
data = pd.DataFrame(eprate.iloc[:,[1,2,4,5]])
# data
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
      <th>averageRating</th>
      <th>numVotes</th>
      <th>seasonNumber</th>
      <th>episodeNumber</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>29</th>
      <td>8.1</td>
      <td>4027</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>49</th>
      <td>8.4</td>
      <td>3546</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>8.1</td>
      <td>3238</td>
      <td>1</td>
      <td>3</td>
    </tr>
    <tr>
      <th>16</th>
      <td>8.3</td>
      <td>3093</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8.2</td>
      <td>2955</td>
      <td>1</td>
      <td>5</td>
    </tr>
    <tr>
      <th>50</th>
      <td>8.0</td>
      <td>2843</td>
      <td>1</td>
      <td>6</td>
    </tr>
    <tr>
      <th>14</th>
      <td>8.1</td>
      <td>2794</td>
      <td>1</td>
      <td>7</td>
    </tr>
    <tr>
      <th>24</th>
      <td>8.0</td>
      <td>2726</td>
      <td>1</td>
      <td>8</td>
    </tr>
    <tr>
      <th>40</th>
      <td>8.4</td>
      <td>2698</td>
      <td>1</td>
      <td>9</td>
    </tr>
    <tr>
      <th>28</th>
      <td>9.1</td>
      <td>3435</td>
      <td>1</td>
      <td>10</td>
    </tr>
    <tr>
      <th>31</th>
      <td>8.2</td>
      <td>2689</td>
      <td>1</td>
      <td>11</td>
    </tr>
    <tr>
      <th>19</th>
      <td>8.4</td>
      <td>2620</td>
      <td>1</td>
      <td>12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8.4</td>
      <td>2592</td>
      <td>1</td>
      <td>13</td>
    </tr>
    <tr>
      <th>37</th>
      <td>8.5</td>
      <td>2696</td>
      <td>1</td>
      <td>14</td>
    </tr>
    <tr>
      <th>39</th>
      <td>8.1</td>
      <td>2520</td>
      <td>1</td>
      <td>15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8.5</td>
      <td>2554</td>
      <td>1</td>
      <td>16</td>
    </tr>
    <tr>
      <th>15</th>
      <td>8.7</td>
      <td>2678</td>
      <td>1</td>
      <td>17</td>
    </tr>
    <tr>
      <th>21</th>
      <td>8.2</td>
      <td>2435</td>
      <td>1</td>
      <td>18</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8.1</td>
      <td>2422</td>
      <td>1</td>
      <td>19</td>
    </tr>
    <tr>
      <th>51</th>
      <td>7.9</td>
      <td>2391</td>
      <td>1</td>
      <td>20</td>
    </tr>
    <tr>
      <th>25</th>
      <td>8.5</td>
      <td>2463</td>
      <td>1</td>
      <td>21</td>
    </tr>
    <tr>
      <th>17</th>
      <td>8.6</td>
      <td>2523</td>
      <td>1</td>
      <td>22</td>
    </tr>
    <tr>
      <th>46</th>
      <td>8.7</td>
      <td>2495</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>47</th>
      <td>8.5</td>
      <td>2443</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8.8</td>
      <td>2604</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>12</th>
      <td>9.0</td>
      <td>2759</td>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <th>36</th>
      <td>8.5</td>
      <td>2318</td>
      <td>2</td>
      <td>5</td>
    </tr>
    <tr>
      <th>0</th>
      <td>9.0</td>
      <td>2850</td>
      <td>2</td>
      <td>6</td>
    </tr>
    <tr>
      <th>41</th>
      <td>8.1</td>
      <td>2225</td>
      <td>2</td>
      <td>7</td>
    </tr>
    <tr>
      <th>32</th>
      <td>8.0</td>
      <td>2186</td>
      <td>2</td>
      <td>8</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8.0</td>
      <td>2200</td>
      <td>2</td>
      <td>9</td>
    </tr>
    <tr>
      <th>33</th>
      <td>8.3</td>
      <td>2333</td>
      <td>2</td>
      <td>10</td>
    </tr>
    <tr>
      <th>27</th>
      <td>8.3</td>
      <td>2183</td>
      <td>2</td>
      <td>11</td>
    </tr>
    <tr>
      <th>13</th>
      <td>8.7</td>
      <td>2301</td>
      <td>2</td>
      <td>12</td>
    </tr>
    <tr>
      <th>22</th>
      <td>8.6</td>
      <td>2329</td>
      <td>2</td>
      <td>13</td>
    </tr>
    <tr>
      <th>44</th>
      <td>8.5</td>
      <td>2242</td>
      <td>2</td>
      <td>14</td>
    </tr>
    <tr>
      <th>48</th>
      <td>8.6</td>
      <td>2294</td>
      <td>2</td>
      <td>15</td>
    </tr>
    <tr>
      <th>20</th>
      <td>9.0</td>
      <td>2635</td>
      <td>2</td>
      <td>16</td>
    </tr>
    <tr>
      <th>38</th>
      <td>8.5</td>
      <td>2183</td>
      <td>2</td>
      <td>17</td>
    </tr>
    <tr>
      <th>34</th>
      <td>8.9</td>
      <td>2319</td>
      <td>2</td>
      <td>18</td>
    </tr>
    <tr>
      <th>43</th>
      <td>8.6</td>
      <td>2236</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>42</th>
      <td>8.3</td>
      <td>2209</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>11</th>
      <td>8.6</td>
      <td>2231</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>26</th>
      <td>8.2</td>
      <td>2188</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>23</th>
      <td>8.7</td>
      <td>2378</td>
      <td>3</td>
      <td>5</td>
    </tr>
    <tr>
      <th>45</th>
      <td>8.6</td>
      <td>2225</td>
      <td>3</td>
      <td>6</td>
    </tr>
    <tr>
      <th>30</th>
      <td>7.9</td>
      <td>2056</td>
      <td>3</td>
      <td>7</td>
    </tr>
    <tr>
      <th>18</th>
      <td>8.7</td>
      <td>2281</td>
      <td>3</td>
      <td>8</td>
    </tr>
    <tr>
      <th>35</th>
      <td>8.7</td>
      <td>2338</td>
      <td>3</td>
      <td>9</td>
    </tr>
    <tr>
      <th>9</th>
      <td>8.5</td>
      <td>2110</td>
      <td>3</td>
      <td>10</td>
    </tr>
    <tr>
      <th>10</th>
      <td>8.6</td>
      <td>2158</td>
      <td>3</td>
      <td>11</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8.8</td>
      <td>2206</td>
      <td>3</td>
      <td>12</td>
    </tr>
    <tr>
      <th>52</th>
      <td>9.2</td>
      <td>2894</td>
      <td>3</td>
      <td>13</td>
    </tr>
    <tr>
      <th>53</th>
      <td>7.3</td>
      <td>2325</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>55</th>
      <td>6.8</td>
      <td>1916</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>56</th>
      <td>6.9</td>
      <td>1805</td>
      <td>4</td>
      <td>3</td>
    </tr>
    <tr>
      <th>57</th>
      <td>7.6</td>
      <td>1694</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>58</th>
      <td>7.6</td>
      <td>1691</td>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>59</th>
      <td>7.1</td>
      <td>1550</td>
      <td>4</td>
      <td>6</td>
    </tr>
    <tr>
      <th>60</th>
      <td>8.2</td>
      <td>1743</td>
      <td>4</td>
      <td>7</td>
    </tr>
    <tr>
      <th>61</th>
      <td>7.5</td>
      <td>1506</td>
      <td>4</td>
      <td>8</td>
    </tr>
    <tr>
      <th>62</th>
      <td>7.6</td>
      <td>1481</td>
      <td>4</td>
      <td>9</td>
    </tr>
    <tr>
      <th>54</th>
      <td>7.6</td>
      <td>1474</td>
      <td>4</td>
      <td>10</td>
    </tr>
    <tr>
      <th>63</th>
      <td>8.4</td>
      <td>1642</td>
      <td>4</td>
      <td>11</td>
    </tr>
    <tr>
      <th>65</th>
      <td>8.1</td>
      <td>1462</td>
      <td>4</td>
      <td>12</td>
    </tr>
    <tr>
      <th>64</th>
      <td>8.1</td>
      <td>1477</td>
      <td>4</td>
      <td>13</td>
    </tr>
    <tr>
      <th>66</th>
      <td>8.0</td>
      <td>1475</td>
      <td>4</td>
      <td>14</td>
    </tr>
    <tr>
      <th>67</th>
      <td>8.1</td>
      <td>1524</td>
      <td>4</td>
      <td>15</td>
    </tr>
    <tr>
      <th>68</th>
      <td>7.0</td>
      <td>1222</td>
      <td>5</td>
      <td>1</td>
    </tr>
    <tr>
      <th>70</th>
      <td>7.1</td>
      <td>1076</td>
      <td>5</td>
      <td>2</td>
    </tr>
    <tr>
      <th>71</th>
      <td>7.3</td>
      <td>1029</td>
      <td>5</td>
      <td>3</td>
    </tr>
    <tr>
      <th>72</th>
      <td>7.3</td>
      <td>997</td>
      <td>5</td>
      <td>4</td>
    </tr>
    <tr>
      <th>73</th>
      <td>7.2</td>
      <td>978</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>74</th>
      <td>7.5</td>
      <td>978</td>
      <td>5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>75</th>
      <td>7.4</td>
      <td>963</td>
      <td>5</td>
      <td>7</td>
    </tr>
    <tr>
      <th>76</th>
      <td>7.3</td>
      <td>965</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>77</th>
      <td>6.9</td>
      <td>818</td>
      <td>5</td>
      <td>9</td>
    </tr>
    <tr>
      <th>78</th>
      <td>6.9</td>
      <td>770</td>
      <td>5</td>
      <td>10</td>
    </tr>
    <tr>
      <th>79</th>
      <td>6.7</td>
      <td>739</td>
      <td>5</td>
      <td>11</td>
    </tr>
    <tr>
      <th>81</th>
      <td>7.4</td>
      <td>753</td>
      <td>5</td>
      <td>12</td>
    </tr>
    <tr>
      <th>80</th>
      <td>6.8</td>
      <td>741</td>
      <td>5</td>
      <td>13</td>
    </tr>
    <tr>
      <th>82</th>
      <td>6.6</td>
      <td>738</td>
      <td>5</td>
      <td>14</td>
    </tr>
    <tr>
      <th>83</th>
      <td>7.0</td>
      <td>733</td>
      <td>5</td>
      <td>15</td>
    </tr>
    <tr>
      <th>69</th>
      <td>7.7</td>
      <td>927</td>
      <td>5</td>
      <td>16</td>
    </tr>
  </tbody>
</table>
</div>




```python
## Here we create a combined column which appends the seasonNumber 
## and episodeNumber of every episode for plotting purposes

for idx in data.index:
    if int(data.at[idx, 'episodeNumber']) < 10:
        data.at[idx, 'episodeNumber'] = "0" + str(data.at[idx, 'episodeNumber'])

data['combined'] = data['seasonNumber'].astype(str) + data['episodeNumber'].astype(str)
# display(data)
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
      <th>averageRating</th>
      <th>numVotes</th>
      <th>seasonNumber</th>
      <th>episodeNumber</th>
      <th>combined</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>29</th>
      <td>8.1</td>
      <td>4027</td>
      <td>1</td>
      <td>01</td>
      <td>101</td>
    </tr>
    <tr>
      <th>49</th>
      <td>8.4</td>
      <td>3546</td>
      <td>1</td>
      <td>02</td>
      <td>102</td>
    </tr>
    <tr>
      <th>5</th>
      <td>8.1</td>
      <td>3238</td>
      <td>1</td>
      <td>03</td>
      <td>103</td>
    </tr>
    <tr>
      <th>16</th>
      <td>8.3</td>
      <td>3093</td>
      <td>1</td>
      <td>04</td>
      <td>104</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8.2</td>
      <td>2955</td>
      <td>1</td>
      <td>05</td>
      <td>105</td>
    </tr>
    <tr>
      <th>50</th>
      <td>8.0</td>
      <td>2843</td>
      <td>1</td>
      <td>06</td>
      <td>106</td>
    </tr>
    <tr>
      <th>14</th>
      <td>8.1</td>
      <td>2794</td>
      <td>1</td>
      <td>07</td>
      <td>107</td>
    </tr>
    <tr>
      <th>24</th>
      <td>8.0</td>
      <td>2726</td>
      <td>1</td>
      <td>08</td>
      <td>108</td>
    </tr>
    <tr>
      <th>40</th>
      <td>8.4</td>
      <td>2698</td>
      <td>1</td>
      <td>09</td>
      <td>109</td>
    </tr>
    <tr>
      <th>28</th>
      <td>9.1</td>
      <td>3435</td>
      <td>1</td>
      <td>10</td>
      <td>110</td>
    </tr>
    <tr>
      <th>31</th>
      <td>8.2</td>
      <td>2689</td>
      <td>1</td>
      <td>11</td>
      <td>111</td>
    </tr>
    <tr>
      <th>19</th>
      <td>8.4</td>
      <td>2620</td>
      <td>1</td>
      <td>12</td>
      <td>112</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8.4</td>
      <td>2592</td>
      <td>1</td>
      <td>13</td>
      <td>113</td>
    </tr>
    <tr>
      <th>37</th>
      <td>8.5</td>
      <td>2696</td>
      <td>1</td>
      <td>14</td>
      <td>114</td>
    </tr>
    <tr>
      <th>39</th>
      <td>8.1</td>
      <td>2520</td>
      <td>1</td>
      <td>15</td>
      <td>115</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8.5</td>
      <td>2554</td>
      <td>1</td>
      <td>16</td>
      <td>116</td>
    </tr>
    <tr>
      <th>15</th>
      <td>8.7</td>
      <td>2678</td>
      <td>1</td>
      <td>17</td>
      <td>117</td>
    </tr>
    <tr>
      <th>21</th>
      <td>8.2</td>
      <td>2435</td>
      <td>1</td>
      <td>18</td>
      <td>118</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8.1</td>
      <td>2422</td>
      <td>1</td>
      <td>19</td>
      <td>119</td>
    </tr>
    <tr>
      <th>51</th>
      <td>7.9</td>
      <td>2391</td>
      <td>1</td>
      <td>20</td>
      <td>120</td>
    </tr>
    <tr>
      <th>25</th>
      <td>8.5</td>
      <td>2463</td>
      <td>1</td>
      <td>21</td>
      <td>121</td>
    </tr>
    <tr>
      <th>17</th>
      <td>8.6</td>
      <td>2523</td>
      <td>1</td>
      <td>22</td>
      <td>122</td>
    </tr>
    <tr>
      <th>46</th>
      <td>8.7</td>
      <td>2495</td>
      <td>2</td>
      <td>01</td>
      <td>201</td>
    </tr>
    <tr>
      <th>47</th>
      <td>8.5</td>
      <td>2443</td>
      <td>2</td>
      <td>02</td>
      <td>202</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8.8</td>
      <td>2604</td>
      <td>2</td>
      <td>03</td>
      <td>203</td>
    </tr>
    <tr>
      <th>12</th>
      <td>9.0</td>
      <td>2759</td>
      <td>2</td>
      <td>04</td>
      <td>204</td>
    </tr>
    <tr>
      <th>36</th>
      <td>8.5</td>
      <td>2318</td>
      <td>2</td>
      <td>05</td>
      <td>205</td>
    </tr>
    <tr>
      <th>0</th>
      <td>9.0</td>
      <td>2850</td>
      <td>2</td>
      <td>06</td>
      <td>206</td>
    </tr>
    <tr>
      <th>41</th>
      <td>8.1</td>
      <td>2225</td>
      <td>2</td>
      <td>07</td>
      <td>207</td>
    </tr>
    <tr>
      <th>32</th>
      <td>8.0</td>
      <td>2186</td>
      <td>2</td>
      <td>08</td>
      <td>208</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8.0</td>
      <td>2200</td>
      <td>2</td>
      <td>09</td>
      <td>209</td>
    </tr>
    <tr>
      <th>33</th>
      <td>8.3</td>
      <td>2333</td>
      <td>2</td>
      <td>10</td>
      <td>210</td>
    </tr>
    <tr>
      <th>27</th>
      <td>8.3</td>
      <td>2183</td>
      <td>2</td>
      <td>11</td>
      <td>211</td>
    </tr>
    <tr>
      <th>13</th>
      <td>8.7</td>
      <td>2301</td>
      <td>2</td>
      <td>12</td>
      <td>212</td>
    </tr>
    <tr>
      <th>22</th>
      <td>8.6</td>
      <td>2329</td>
      <td>2</td>
      <td>13</td>
      <td>213</td>
    </tr>
    <tr>
      <th>44</th>
      <td>8.5</td>
      <td>2242</td>
      <td>2</td>
      <td>14</td>
      <td>214</td>
    </tr>
    <tr>
      <th>48</th>
      <td>8.6</td>
      <td>2294</td>
      <td>2</td>
      <td>15</td>
      <td>215</td>
    </tr>
    <tr>
      <th>20</th>
      <td>9.0</td>
      <td>2635</td>
      <td>2</td>
      <td>16</td>
      <td>216</td>
    </tr>
    <tr>
      <th>38</th>
      <td>8.5</td>
      <td>2183</td>
      <td>2</td>
      <td>17</td>
      <td>217</td>
    </tr>
    <tr>
      <th>34</th>
      <td>8.9</td>
      <td>2319</td>
      <td>2</td>
      <td>18</td>
      <td>218</td>
    </tr>
    <tr>
      <th>43</th>
      <td>8.6</td>
      <td>2236</td>
      <td>3</td>
      <td>01</td>
      <td>301</td>
    </tr>
    <tr>
      <th>42</th>
      <td>8.3</td>
      <td>2209</td>
      <td>3</td>
      <td>02</td>
      <td>302</td>
    </tr>
    <tr>
      <th>11</th>
      <td>8.6</td>
      <td>2231</td>
      <td>3</td>
      <td>03</td>
      <td>303</td>
    </tr>
    <tr>
      <th>26</th>
      <td>8.2</td>
      <td>2188</td>
      <td>3</td>
      <td>04</td>
      <td>304</td>
    </tr>
    <tr>
      <th>23</th>
      <td>8.7</td>
      <td>2378</td>
      <td>3</td>
      <td>05</td>
      <td>305</td>
    </tr>
    <tr>
      <th>45</th>
      <td>8.6</td>
      <td>2225</td>
      <td>3</td>
      <td>06</td>
      <td>306</td>
    </tr>
    <tr>
      <th>30</th>
      <td>7.9</td>
      <td>2056</td>
      <td>3</td>
      <td>07</td>
      <td>307</td>
    </tr>
    <tr>
      <th>18</th>
      <td>8.7</td>
      <td>2281</td>
      <td>3</td>
      <td>08</td>
      <td>308</td>
    </tr>
    <tr>
      <th>35</th>
      <td>8.7</td>
      <td>2338</td>
      <td>3</td>
      <td>09</td>
      <td>309</td>
    </tr>
    <tr>
      <th>9</th>
      <td>8.5</td>
      <td>2110</td>
      <td>3</td>
      <td>10</td>
      <td>310</td>
    </tr>
    <tr>
      <th>10</th>
      <td>8.6</td>
      <td>2158</td>
      <td>3</td>
      <td>11</td>
      <td>311</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8.8</td>
      <td>2206</td>
      <td>3</td>
      <td>12</td>
      <td>312</td>
    </tr>
    <tr>
      <th>52</th>
      <td>9.2</td>
      <td>2894</td>
      <td>3</td>
      <td>13</td>
      <td>313</td>
    </tr>
    <tr>
      <th>53</th>
      <td>7.3</td>
      <td>2325</td>
      <td>4</td>
      <td>01</td>
      <td>401</td>
    </tr>
    <tr>
      <th>55</th>
      <td>6.8</td>
      <td>1916</td>
      <td>4</td>
      <td>02</td>
      <td>402</td>
    </tr>
    <tr>
      <th>56</th>
      <td>6.9</td>
      <td>1805</td>
      <td>4</td>
      <td>03</td>
      <td>403</td>
    </tr>
    <tr>
      <th>57</th>
      <td>7.6</td>
      <td>1694</td>
      <td>4</td>
      <td>04</td>
      <td>404</td>
    </tr>
    <tr>
      <th>58</th>
      <td>7.6</td>
      <td>1691</td>
      <td>4</td>
      <td>05</td>
      <td>405</td>
    </tr>
    <tr>
      <th>59</th>
      <td>7.1</td>
      <td>1550</td>
      <td>4</td>
      <td>06</td>
      <td>406</td>
    </tr>
    <tr>
      <th>60</th>
      <td>8.2</td>
      <td>1743</td>
      <td>4</td>
      <td>07</td>
      <td>407</td>
    </tr>
    <tr>
      <th>61</th>
      <td>7.5</td>
      <td>1506</td>
      <td>4</td>
      <td>08</td>
      <td>408</td>
    </tr>
    <tr>
      <th>62</th>
      <td>7.6</td>
      <td>1481</td>
      <td>4</td>
      <td>09</td>
      <td>409</td>
    </tr>
    <tr>
      <th>54</th>
      <td>7.6</td>
      <td>1474</td>
      <td>4</td>
      <td>10</td>
      <td>410</td>
    </tr>
    <tr>
      <th>63</th>
      <td>8.4</td>
      <td>1642</td>
      <td>4</td>
      <td>11</td>
      <td>411</td>
    </tr>
    <tr>
      <th>65</th>
      <td>8.1</td>
      <td>1462</td>
      <td>4</td>
      <td>12</td>
      <td>412</td>
    </tr>
    <tr>
      <th>64</th>
      <td>8.1</td>
      <td>1477</td>
      <td>4</td>
      <td>13</td>
      <td>413</td>
    </tr>
    <tr>
      <th>66</th>
      <td>8.0</td>
      <td>1475</td>
      <td>4</td>
      <td>14</td>
      <td>414</td>
    </tr>
    <tr>
      <th>67</th>
      <td>8.1</td>
      <td>1524</td>
      <td>4</td>
      <td>15</td>
      <td>415</td>
    </tr>
    <tr>
      <th>68</th>
      <td>7.0</td>
      <td>1222</td>
      <td>5</td>
      <td>01</td>
      <td>501</td>
    </tr>
    <tr>
      <th>70</th>
      <td>7.1</td>
      <td>1076</td>
      <td>5</td>
      <td>02</td>
      <td>502</td>
    </tr>
    <tr>
      <th>71</th>
      <td>7.3</td>
      <td>1029</td>
      <td>5</td>
      <td>03</td>
      <td>503</td>
    </tr>
    <tr>
      <th>72</th>
      <td>7.3</td>
      <td>997</td>
      <td>5</td>
      <td>04</td>
      <td>504</td>
    </tr>
    <tr>
      <th>73</th>
      <td>7.2</td>
      <td>978</td>
      <td>5</td>
      <td>05</td>
      <td>505</td>
    </tr>
    <tr>
      <th>74</th>
      <td>7.5</td>
      <td>978</td>
      <td>5</td>
      <td>06</td>
      <td>506</td>
    </tr>
    <tr>
      <th>75</th>
      <td>7.4</td>
      <td>963</td>
      <td>5</td>
      <td>07</td>
      <td>507</td>
    </tr>
    <tr>
      <th>76</th>
      <td>7.3</td>
      <td>965</td>
      <td>5</td>
      <td>08</td>
      <td>508</td>
    </tr>
    <tr>
      <th>77</th>
      <td>6.9</td>
      <td>818</td>
      <td>5</td>
      <td>09</td>
      <td>509</td>
    </tr>
    <tr>
      <th>78</th>
      <td>6.9</td>
      <td>770</td>
      <td>5</td>
      <td>10</td>
      <td>510</td>
    </tr>
    <tr>
      <th>79</th>
      <td>6.7</td>
      <td>739</td>
      <td>5</td>
      <td>11</td>
      <td>511</td>
    </tr>
    <tr>
      <th>81</th>
      <td>7.4</td>
      <td>753</td>
      <td>5</td>
      <td>12</td>
      <td>512</td>
    </tr>
    <tr>
      <th>80</th>
      <td>6.8</td>
      <td>741</td>
      <td>5</td>
      <td>13</td>
      <td>513</td>
    </tr>
    <tr>
      <th>82</th>
      <td>6.6</td>
      <td>738</td>
      <td>5</td>
      <td>14</td>
      <td>514</td>
    </tr>
    <tr>
      <th>83</th>
      <td>7.0</td>
      <td>733</td>
      <td>5</td>
      <td>15</td>
      <td>515</td>
    </tr>
    <tr>
      <th>69</th>
      <td>7.7</td>
      <td>927</td>
      <td>5</td>
      <td>16</td>
      <td>516</td>
    </tr>
  </tbody>
</table>
</div>


STEP 3: DATA ANALYSIS & VISUALIZATION


```python
## Imports
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.linear_model import LinearRegression
import numpy as np
import statsmodels.api as sm
import statsmodels.formula.api as smf
```


```python
print(data.describe()) # Descriptive statistics 
```

           averageRating     numVotes  seasonNumber            sd
    count      84.000000    84.000000     84.000000  8.400000e+01
    mean        8.061905  2065.940476      2.821429  6.463810e-01
    std         0.646381   736.040602      1.482108  1.116891e-16
    min         6.600000   733.000000      1.000000  6.463810e-01
    25%         7.600000  1499.750000      1.000000  6.463810e-01
    50%         8.200000  2228.000000      3.000000  6.463810e-01
    75%         8.525000  2530.750000      4.000000  6.463810e-01
    max         9.200000  4027.000000      5.000000  6.463810e-01



```python
season_ep_count={'S1 Episode Count':0, 'S2 Episode Count':0, 'S3 Episode Count':0, 'S4 Episode Count':0, 'S5 Episode Count':0}
for entry in data['seasonNumber']:
    if entry == 1:
        season_ep_count['S1 Episode Count'] +=1
    elif entry == 2:
        season_ep_count['S2 Episode Count'] +=1
    elif entry == 3:
        season_ep_count['S3 Episode Count'] +=1
    elif entry == 4:
        season_ep_count['S4 Episode Count'] +=1
    else:
        season_ep_count['S5 Episode Count'] +=1
season_ep_count
```




    {'S1 Episode Count': 22,
     'S2 Episode Count': 18,
     'S3 Episode Count': 13,
     'S4 Episode Count': 15,
     'S5 Episode Count': 16}




```python
## Divide the dataset into the 5 seasons
s1_data = data.iloc[0:22]
s2_data = data.iloc[22:40]
s3_data = data.iloc[40:53]
s4_data = data.iloc[53:68]
s5_data = data.iloc[68:84]
display(s1_data,s2_data,s3_data,s4_data,s5_data)
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
      <th>averageRating</th>
      <th>numVotes</th>
      <th>seasonNumber</th>
      <th>episodeNumber</th>
      <th>combined</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>29</th>
      <td>8.1</td>
      <td>4027</td>
      <td>1</td>
      <td>01</td>
      <td>101</td>
    </tr>
    <tr>
      <th>49</th>
      <td>8.4</td>
      <td>3546</td>
      <td>1</td>
      <td>02</td>
      <td>102</td>
    </tr>
    <tr>
      <th>5</th>
      <td>8.1</td>
      <td>3238</td>
      <td>1</td>
      <td>03</td>
      <td>103</td>
    </tr>
    <tr>
      <th>16</th>
      <td>8.3</td>
      <td>3093</td>
      <td>1</td>
      <td>04</td>
      <td>104</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8.2</td>
      <td>2955</td>
      <td>1</td>
      <td>05</td>
      <td>105</td>
    </tr>
    <tr>
      <th>50</th>
      <td>8.0</td>
      <td>2843</td>
      <td>1</td>
      <td>06</td>
      <td>106</td>
    </tr>
    <tr>
      <th>14</th>
      <td>8.1</td>
      <td>2794</td>
      <td>1</td>
      <td>07</td>
      <td>107</td>
    </tr>
    <tr>
      <th>24</th>
      <td>8.0</td>
      <td>2726</td>
      <td>1</td>
      <td>08</td>
      <td>108</td>
    </tr>
    <tr>
      <th>40</th>
      <td>8.4</td>
      <td>2698</td>
      <td>1</td>
      <td>09</td>
      <td>109</td>
    </tr>
    <tr>
      <th>28</th>
      <td>9.1</td>
      <td>3435</td>
      <td>1</td>
      <td>10</td>
      <td>110</td>
    </tr>
    <tr>
      <th>31</th>
      <td>8.2</td>
      <td>2689</td>
      <td>1</td>
      <td>11</td>
      <td>111</td>
    </tr>
    <tr>
      <th>19</th>
      <td>8.4</td>
      <td>2620</td>
      <td>1</td>
      <td>12</td>
      <td>112</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8.4</td>
      <td>2592</td>
      <td>1</td>
      <td>13</td>
      <td>113</td>
    </tr>
    <tr>
      <th>37</th>
      <td>8.5</td>
      <td>2696</td>
      <td>1</td>
      <td>14</td>
      <td>114</td>
    </tr>
    <tr>
      <th>39</th>
      <td>8.1</td>
      <td>2520</td>
      <td>1</td>
      <td>15</td>
      <td>115</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8.5</td>
      <td>2554</td>
      <td>1</td>
      <td>16</td>
      <td>116</td>
    </tr>
    <tr>
      <th>15</th>
      <td>8.7</td>
      <td>2678</td>
      <td>1</td>
      <td>17</td>
      <td>117</td>
    </tr>
    <tr>
      <th>21</th>
      <td>8.2</td>
      <td>2435</td>
      <td>1</td>
      <td>18</td>
      <td>118</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8.1</td>
      <td>2422</td>
      <td>1</td>
      <td>19</td>
      <td>119</td>
    </tr>
    <tr>
      <th>51</th>
      <td>7.9</td>
      <td>2391</td>
      <td>1</td>
      <td>20</td>
      <td>120</td>
    </tr>
    <tr>
      <th>25</th>
      <td>8.5</td>
      <td>2463</td>
      <td>1</td>
      <td>21</td>
      <td>121</td>
    </tr>
    <tr>
      <th>17</th>
      <td>8.6</td>
      <td>2523</td>
      <td>1</td>
      <td>22</td>
      <td>122</td>
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
      <th>averageRating</th>
      <th>numVotes</th>
      <th>seasonNumber</th>
      <th>episodeNumber</th>
      <th>combined</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>46</th>
      <td>8.7</td>
      <td>2495</td>
      <td>2</td>
      <td>01</td>
      <td>201</td>
    </tr>
    <tr>
      <th>47</th>
      <td>8.5</td>
      <td>2443</td>
      <td>2</td>
      <td>02</td>
      <td>202</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8.8</td>
      <td>2604</td>
      <td>2</td>
      <td>03</td>
      <td>203</td>
    </tr>
    <tr>
      <th>12</th>
      <td>9.0</td>
      <td>2759</td>
      <td>2</td>
      <td>04</td>
      <td>204</td>
    </tr>
    <tr>
      <th>36</th>
      <td>8.5</td>
      <td>2318</td>
      <td>2</td>
      <td>05</td>
      <td>205</td>
    </tr>
    <tr>
      <th>0</th>
      <td>9.0</td>
      <td>2850</td>
      <td>2</td>
      <td>06</td>
      <td>206</td>
    </tr>
    <tr>
      <th>41</th>
      <td>8.1</td>
      <td>2225</td>
      <td>2</td>
      <td>07</td>
      <td>207</td>
    </tr>
    <tr>
      <th>32</th>
      <td>8.0</td>
      <td>2186</td>
      <td>2</td>
      <td>08</td>
      <td>208</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8.0</td>
      <td>2200</td>
      <td>2</td>
      <td>09</td>
      <td>209</td>
    </tr>
    <tr>
      <th>33</th>
      <td>8.3</td>
      <td>2333</td>
      <td>2</td>
      <td>10</td>
      <td>210</td>
    </tr>
    <tr>
      <th>27</th>
      <td>8.3</td>
      <td>2183</td>
      <td>2</td>
      <td>11</td>
      <td>211</td>
    </tr>
    <tr>
      <th>13</th>
      <td>8.7</td>
      <td>2301</td>
      <td>2</td>
      <td>12</td>
      <td>212</td>
    </tr>
    <tr>
      <th>22</th>
      <td>8.6</td>
      <td>2329</td>
      <td>2</td>
      <td>13</td>
      <td>213</td>
    </tr>
    <tr>
      <th>44</th>
      <td>8.5</td>
      <td>2242</td>
      <td>2</td>
      <td>14</td>
      <td>214</td>
    </tr>
    <tr>
      <th>48</th>
      <td>8.6</td>
      <td>2294</td>
      <td>2</td>
      <td>15</td>
      <td>215</td>
    </tr>
    <tr>
      <th>20</th>
      <td>9.0</td>
      <td>2635</td>
      <td>2</td>
      <td>16</td>
      <td>216</td>
    </tr>
    <tr>
      <th>38</th>
      <td>8.5</td>
      <td>2183</td>
      <td>2</td>
      <td>17</td>
      <td>217</td>
    </tr>
    <tr>
      <th>34</th>
      <td>8.9</td>
      <td>2319</td>
      <td>2</td>
      <td>18</td>
      <td>218</td>
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
      <th>averageRating</th>
      <th>numVotes</th>
      <th>seasonNumber</th>
      <th>episodeNumber</th>
      <th>combined</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>43</th>
      <td>8.6</td>
      <td>2236</td>
      <td>3</td>
      <td>01</td>
      <td>301</td>
    </tr>
    <tr>
      <th>42</th>
      <td>8.3</td>
      <td>2209</td>
      <td>3</td>
      <td>02</td>
      <td>302</td>
    </tr>
    <tr>
      <th>11</th>
      <td>8.6</td>
      <td>2231</td>
      <td>3</td>
      <td>03</td>
      <td>303</td>
    </tr>
    <tr>
      <th>26</th>
      <td>8.2</td>
      <td>2188</td>
      <td>3</td>
      <td>04</td>
      <td>304</td>
    </tr>
    <tr>
      <th>23</th>
      <td>8.7</td>
      <td>2378</td>
      <td>3</td>
      <td>05</td>
      <td>305</td>
    </tr>
    <tr>
      <th>45</th>
      <td>8.6</td>
      <td>2225</td>
      <td>3</td>
      <td>06</td>
      <td>306</td>
    </tr>
    <tr>
      <th>30</th>
      <td>7.9</td>
      <td>2056</td>
      <td>3</td>
      <td>07</td>
      <td>307</td>
    </tr>
    <tr>
      <th>18</th>
      <td>8.7</td>
      <td>2281</td>
      <td>3</td>
      <td>08</td>
      <td>308</td>
    </tr>
    <tr>
      <th>35</th>
      <td>8.7</td>
      <td>2338</td>
      <td>3</td>
      <td>09</td>
      <td>309</td>
    </tr>
    <tr>
      <th>9</th>
      <td>8.5</td>
      <td>2110</td>
      <td>3</td>
      <td>10</td>
      <td>310</td>
    </tr>
    <tr>
      <th>10</th>
      <td>8.6</td>
      <td>2158</td>
      <td>3</td>
      <td>11</td>
      <td>311</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8.8</td>
      <td>2206</td>
      <td>3</td>
      <td>12</td>
      <td>312</td>
    </tr>
    <tr>
      <th>52</th>
      <td>9.2</td>
      <td>2894</td>
      <td>3</td>
      <td>13</td>
      <td>313</td>
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
      <th>averageRating</th>
      <th>numVotes</th>
      <th>seasonNumber</th>
      <th>episodeNumber</th>
      <th>combined</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>53</th>
      <td>7.3</td>
      <td>2325</td>
      <td>4</td>
      <td>01</td>
      <td>401</td>
    </tr>
    <tr>
      <th>55</th>
      <td>6.8</td>
      <td>1916</td>
      <td>4</td>
      <td>02</td>
      <td>402</td>
    </tr>
    <tr>
      <th>56</th>
      <td>6.9</td>
      <td>1805</td>
      <td>4</td>
      <td>03</td>
      <td>403</td>
    </tr>
    <tr>
      <th>57</th>
      <td>7.6</td>
      <td>1694</td>
      <td>4</td>
      <td>04</td>
      <td>404</td>
    </tr>
    <tr>
      <th>58</th>
      <td>7.6</td>
      <td>1691</td>
      <td>4</td>
      <td>05</td>
      <td>405</td>
    </tr>
    <tr>
      <th>59</th>
      <td>7.1</td>
      <td>1550</td>
      <td>4</td>
      <td>06</td>
      <td>406</td>
    </tr>
    <tr>
      <th>60</th>
      <td>8.2</td>
      <td>1743</td>
      <td>4</td>
      <td>07</td>
      <td>407</td>
    </tr>
    <tr>
      <th>61</th>
      <td>7.5</td>
      <td>1506</td>
      <td>4</td>
      <td>08</td>
      <td>408</td>
    </tr>
    <tr>
      <th>62</th>
      <td>7.6</td>
      <td>1481</td>
      <td>4</td>
      <td>09</td>
      <td>409</td>
    </tr>
    <tr>
      <th>54</th>
      <td>7.6</td>
      <td>1474</td>
      <td>4</td>
      <td>10</td>
      <td>410</td>
    </tr>
    <tr>
      <th>63</th>
      <td>8.4</td>
      <td>1642</td>
      <td>4</td>
      <td>11</td>
      <td>411</td>
    </tr>
    <tr>
      <th>65</th>
      <td>8.1</td>
      <td>1462</td>
      <td>4</td>
      <td>12</td>
      <td>412</td>
    </tr>
    <tr>
      <th>64</th>
      <td>8.1</td>
      <td>1477</td>
      <td>4</td>
      <td>13</td>
      <td>413</td>
    </tr>
    <tr>
      <th>66</th>
      <td>8.0</td>
      <td>1475</td>
      <td>4</td>
      <td>14</td>
      <td>414</td>
    </tr>
    <tr>
      <th>67</th>
      <td>8.1</td>
      <td>1524</td>
      <td>4</td>
      <td>15</td>
      <td>415</td>
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
      <th>averageRating</th>
      <th>numVotes</th>
      <th>seasonNumber</th>
      <th>episodeNumber</th>
      <th>combined</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>68</th>
      <td>7.0</td>
      <td>1222</td>
      <td>5</td>
      <td>01</td>
      <td>501</td>
    </tr>
    <tr>
      <th>70</th>
      <td>7.1</td>
      <td>1076</td>
      <td>5</td>
      <td>02</td>
      <td>502</td>
    </tr>
    <tr>
      <th>71</th>
      <td>7.3</td>
      <td>1029</td>
      <td>5</td>
      <td>03</td>
      <td>503</td>
    </tr>
    <tr>
      <th>72</th>
      <td>7.3</td>
      <td>997</td>
      <td>5</td>
      <td>04</td>
      <td>504</td>
    </tr>
    <tr>
      <th>73</th>
      <td>7.2</td>
      <td>978</td>
      <td>5</td>
      <td>05</td>
      <td>505</td>
    </tr>
    <tr>
      <th>74</th>
      <td>7.5</td>
      <td>978</td>
      <td>5</td>
      <td>06</td>
      <td>506</td>
    </tr>
    <tr>
      <th>75</th>
      <td>7.4</td>
      <td>963</td>
      <td>5</td>
      <td>07</td>
      <td>507</td>
    </tr>
    <tr>
      <th>76</th>
      <td>7.3</td>
      <td>965</td>
      <td>5</td>
      <td>08</td>
      <td>508</td>
    </tr>
    <tr>
      <th>77</th>
      <td>6.9</td>
      <td>818</td>
      <td>5</td>
      <td>09</td>
      <td>509</td>
    </tr>
    <tr>
      <th>78</th>
      <td>6.9</td>
      <td>770</td>
      <td>5</td>
      <td>10</td>
      <td>510</td>
    </tr>
    <tr>
      <th>79</th>
      <td>6.7</td>
      <td>739</td>
      <td>5</td>
      <td>11</td>
      <td>511</td>
    </tr>
    <tr>
      <th>81</th>
      <td>7.4</td>
      <td>753</td>
      <td>5</td>
      <td>12</td>
      <td>512</td>
    </tr>
    <tr>
      <th>80</th>
      <td>6.8</td>
      <td>741</td>
      <td>5</td>
      <td>13</td>
      <td>513</td>
    </tr>
    <tr>
      <th>82</th>
      <td>6.6</td>
      <td>738</td>
      <td>5</td>
      <td>14</td>
      <td>514</td>
    </tr>
    <tr>
      <th>83</th>
      <td>7.0</td>
      <td>733</td>
      <td>5</td>
      <td>15</td>
      <td>515</td>
    </tr>
    <tr>
      <th>69</th>
      <td>7.7</td>
      <td>927</td>
      <td>5</td>
      <td>16</td>
      <td>516</td>
    </tr>
  </tbody>
</table>
</div>



```python
## First iteration plot: general shape of the data
plt.plot(data['combined'],data['averageRating'], label='averageRating')
plt.xlabel('Episode')
plt.ylabel('Rating')
plt.title('Arrested Development Ratings by Episode')
# plt.grid(True)
plt.legend()
plt.savefig('A_D_Performance_Beginning.png')
```


    
![png](output_15_0.png)
    



```python
## Second iteration plots: testing different plot types
fig, axes = plt.subplots(1,2)
axes[0].hist(data['averageRating'])
# axes[1].scatter(data['combined'], data['averageRating'])
axes[1].plot(data['combined'], data['averageRating'])
fig.savefig('A_D_Performance_Hist_andLine.png')
```


    
![png](output_16_0.png)
    



```python
sns.catplot(x='seasonNumber', y='numVotes', kind='violin', data=data) 
```




    <seaborn.axisgrid.FacetGrid at 0x2a168c3d0>




    
![png](output_17_1.png)
    



```python
## Third iteration plot: scatterplot view of data, colored by season
sns.set() # 
sns.relplot(x='combined', y='averageRating', size='numVotes', sizes=(50,200), hue='seasonNumber', data=data) 
plt.savefig('A_D_Performance_Scatter.png')
# Alternate view:
# sns.relplot(x='combined', y='averageRating', hue='numVotes', col='seasonNumber', data=data) # Full view scatterplot 
# For above code, include col='seasonNumber' if want to display all 5 seasons side by side. Q: Do the attributes
# between these resulting plots have to be shared or can we adjust things like color?
```


    
![png](output_18_0.png)
    



```python
## 4th iteration plot: line graph view of data, divided by season
sns.relplot(
    data=data, x="episodeNumber", y="averageRating", col="seasonNumber",
    hue="seasonNumber",palette='pastel', kind="line", linewidth=6
)
plt.savefig('A_D_Performance_Line_Div.png')
```


    
![png](output_19_0.png)
    



```python
plt.figure(figsize=(20,10))
sns.scatterplot(data=data, x='combined', y='averageRating', hue='seasonNumber',palette='pastel', size='numVotes', sizes=(80,600), legend=True)
sns.lineplot(data=data, x='combined', y='averageRating', estimator='max', hue='seasonNumber',palette='pastel', legend=False)
plt.axhline(data['averageRating'].mean(), color='gray', linestyle='--', linewidth=3, label='Mean')
font = {'family': 'serif',
        'color':  'black',
        'weight': 'bold',
        'size': 26,
        }
plt.title("Arrested Development Popularity by Episode", fontdict=font)
font['size']=20 # Update the font size
font['weight'] = 0 # Update =the font weight
plt.ylabel("Average Rating", fontdict=font, style='italic'), plt.xlabel("Episode",fontdict=font,style='italic')
plt.ylim(6.5,9.5)
plt.xticks(data['combined'][::11])
plt.grid(False)
plt.legend(bbox_to_anchor=(1.0, 1.0), frameon=False, handlelength=1.0, handleheight=1.5)
plt.tight_layout()
plt.savefig('A_D_Popularity.png')
```


    
![png](output_20_0.png)
    



```python
## Grand mean and standard deviation
data_mean = data['averageRating'].mean()
data_std = data['averageRating'].std()
```


```python
## In this section, we plot each season's average ratings, fit a 4th-degree polynomial to the data, 
## plot the rolling mean by season, and mark the data points which fall outside of one standard 
## deviation from the season's mean.

season_data = [s1_data, s2_data, s3_data, s4_data, s5_data]
fig, axs = plt.subplots(ncols=5,figsize=(80, 15))
color_arr = {
    0:'green',
    1:'blue',
    2:'orange',
    3:'red',
    4:'magenta'
}

axs[0].set_ylabel('Average Ratings', style='italic', weight='bold', fontsize=30)
for i, s_data in enumerate(season_data):
    xs = s_data['episodeNumber'].astype(int)
    ys = s_data['averageRating']
    
    coeff = np.polyfit(xs,ys,deg=4)
    fit = np.polyval(coeff,xs)
    residuals = ys - fit
    std = np.std(residuals)
    
    s_data_mean = s_data['averageRating'].mean()
    s_data_std = s_data['averageRating'].std()
    below_mean = ys < (s_data_mean-s_data_std)
    below_mean_xs = xs[below_mean]
    below_mean_ys = ys[below_mean]
    axs[i].scatter(below_mean_xs, below_mean_ys, color='black', marker='o', s=1450)
    
    above_mean = ys > (s_data_mean+s_data_std)
    above_mean_xs = xs[above_mean]
    above_mean_ys = ys[above_mean]
    axs[i].scatter(above_mean_xs, above_mean_ys, color='black', marker='o', s=1450, label='One SD ± Season Mean')
    

    axs[i].set_title(f'Season {i+1}', fontsize=65, weight='bold',family='serif')
    axs[i].set_titlesize = 30
    axs[i].set_ylim(6.5,9.5)    
    axs[i].set_xlabel('Episodes', style='italic', weight='bold', fontsize=40)
    axs[0].set_ylabel('Average Ratings', style='italic', weight='bold', fontsize=40)
    axs[i].tick_params(axis='both', which='major', labelsize=28)
    axs[i].grid(False)
    axs[i].plot(xs, ys, 'o', color=color_arr[i], markersize=30) # size='numVotes'
    axs[i].plot(xs, fit, color=color_arr[i], label='Fitted Lines', linewidth=18)
    axs[i].fill_between(xs, fit - std, fit + std, color='gray', alpha=0.3) # label='1 Std. Dev.'
    axs[i].axhline(s_data['averageRating'].mean(), color='gray', linestyle='--', linewidth=5, label='Season Means')
    axs[0].legend(loc='lower left')

fig.tight_layout()    
plt.savefig('A_D_Performance_Season_Mean.png')
```


    
![png](output_22_0.png)
    


From the above plots, we see some outlier data in both positive and negative directions (from the account of someone seeking the highest ratings). Seasons 1 and 2 were a bit oscillatory, with just a few standout best and worst moments. Season 3 begins as strongly as season 2 ended, and we see some steady growth until the end, where on the season 3 finale the show achieves its highest rating across the board. 

Additionally, see a large delta in the performances of seasons 1-3 versus the performances of seasons 4-5. Noticeably, the mean line by each season is relatively stable until we reach season 4, where it drops considerably, then again in season 5. One explanation for this drop could be that the show was canceled in its third season, before it achieved its critical acclaim and cultish fame that would later ignite its renewal. Some seven-ish years after the end of the third season began the continuation of the show, with many of the original cast reprising their roles. A gap as long as this has the power to disrupt the viewer's immersion in a show. Because season 3 was slated to be their final season, the show very clearly reaches a satisfying conclusion. To then pick the show back up years later makes for a less fluid transition between seasons, as for example, the experience of seeing some of the characters aged and in vastly different areas of their lives. 

Evident in the data, season 4 starts slow but reaches a modest performance level, featuring the most linear trend across all of the seasons. While Arrested Development is clearly at its peak in seasons 1-3, based on this data, season 4 is worth considering. Season 5, we’ll get to.


```python
## Finally, we end by plotting each season's average ratings alongside the grand mean, fit a 4th-degree 
## polynomial to the data, and, once again, mark data the points which fall outside of one 
## deviation from the grand mean.

season_data = [s1_data, s2_data, s3_data, s4_data, s5_data]
fig, axs = plt.subplots(ncols=5, figsize=(80,15))
color_arr = {
    0:'green',
    1:'blue',
    2:'orange',
    3:'red',
    4:'magenta'
}

axs[0].set_ylabel('Average Ratings', style='italic', weight='bold', fontsize=30)
for i, s_data in enumerate(season_data):
    xs = s_data['episodeNumber'].astype(int)
    ys = s_data['averageRating']
    
    coeff = np.polyfit(xs,ys,deg=4)
    fit = np.polyval(coeff,xs)
    residuals = ys - fit
    std = np.std(residuals)
    
    data_mean = data['averageRating'].mean()
    data_std = data['averageRating'].std()
    below_mean = ys < (data_mean-data_std)
    below_mean_xs = xs[below_mean]
    below_mean_ys = ys[below_mean]
    axs[i].scatter(below_mean_xs, below_mean_ys, color='black', marker='o', s=1450)
    
    above_mean = ys > (data_mean+data_std)
    above_mean_xs = xs[above_mean]
    above_mean_ys = ys[above_mean]
    axs[i].scatter(above_mean_xs, above_mean_ys, color='black', marker='o', s=1450, label='One SD ± Grand Mean')
    

    axs[i].set_title(f'Season {i+1}', fontsize=65, weight='bold',family='serif')
    axs[i].set_titlesize = 30
    axs[i].set_ylim(6.5,9.5)    
    axs[i].set_xlabel('Episodes', style='italic', weight='bold', fontsize=40)
    axs[0].set_ylabel('Average Ratings', style='italic', weight='bold', fontsize=40)
    axs[i].tick_params(axis='both', which='major', labelsize=28)
    axs[i].grid(False)
    axs[i].plot(xs, ys, 'o', color=color_arr[i], markersize=30) # size='numVotes'
    axs[i].plot(xs, fit, color=color_arr[i], label='Fitted Lines', linewidth=18)
    axs[i].fill_between(xs, fit - std, fit + std, color='gray', alpha=0.3) # label='1 Std. Dev.'
    axs[i].axhline(data['averageRating'].mean(), color='gray', linestyle='--', linewidth=5, label='Grand Mean')
    axs[0].legend(loc='lower left')
    
fig.tight_layout()    
plt.savefig('A_D_Performance_Grand_Mean.png')
```


    
![png](output_24_0.png)
    


Now we see a grand mean line plotted against the same data as before. Our highlighted points now vary from the previous graphs as we look for the data that lie outside of 1 standard deviation from the grand mean. Immediately, we see that the only points outside this range are the highest rated episodes of the show, those contained in seasons 1-3. Season 4’s slow start consists of the first batch of low-rated episodes of the show, but holistically, season 4 greatly outperforms season 5. By proportion of episodes below one standard deviation of the mean, we see ~26.67% (4/15) of season 4 episodes occupying this space, in comparison to the 87.50% (14/16) of season 5 episodes that meet the same criteria. Empirically, season 5 is not worth anyone’s time save maybe the completionist. Perhaps it is up for debate whether season 4 is worthy of sharing the spotlight with seasons 1-3. Undoubtedly, seasons 1-3 and seasons 4-5 feel like different shows and so it is up to the viewer if they wish to subject themselves to what is made of this prolific show. Season 3 ends nicely, as we’ve proved, and it is within that vein that we could simply pretend nothing comes after that. Ignorance is bliss as they say.
