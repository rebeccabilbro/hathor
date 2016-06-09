

```python
import pandas as pd
```


```python
PATH = "../data/u.item"
df = pd.read_csv(PATH, names=('movie_id', 'title','release_date'), sep='|', usecols=[0,1,2], encoding = "ISO-8859-1", index_col='movie_id')
df.head(5)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>release_date</th>
    </tr>
    <tr>
      <th>movie_id</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Toy Story (1995)</td>
      <td>01-Jan-1995</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GoldenEye (1995)</td>
      <td>01-Jan-1995</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Four Rooms (1995)</td>
      <td>01-Jan-1995</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Get Shorty (1995)</td>
      <td>01-Jan-1995</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Copycat (1995)</td>
      <td>01-Jan-1995</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['title'] = df['title'].str.replace(r"\(.*\)","")
df.head(5)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>release_date</th>
    </tr>
    <tr>
      <th>movie_id</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Toy Story</td>
      <td>01-Jan-1995</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GoldenEye</td>
      <td>01-Jan-1995</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Four Rooms</td>
      <td>01-Jan-1995</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Get Shorty</td>
      <td>01-Jan-1995</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Copycat</td>
      <td>01-Jan-1995</td>
    </tr>
  </tbody>
</table>
</div>



### What's the oldest movie in the list?


```python
df['release_date'] = pd.to_datetime(df['release_date'])
df.sort_values('release_date').head(1)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>release_date</th>
    </tr>
    <tr>
      <th>movie_id</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>675</th>
      <td>Nosferatu</td>
      <td>1922-01-01</td>
    </tr>
  </tbody>
</table>
</div>



### What's the newest movie in the list?


```python
df.sort_values('release_date', ascending=False).head(1)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>release_date</th>
    </tr>
    <tr>
      <th>movie_id</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>315</th>
      <td>Apt Pupil</td>
      <td>1998-10-23</td>
    </tr>
  </tbody>
</table>
</div>



### How many unique movie titles are there?


```python
# All titles
len(df['title'])
```




    1682




```python
# Unique titles 
len(df['title'].unique())
```




    1658



### Which titles have been repeated?


```python
titles = df["title"]
repeated = df[titles.isin(titles[titles.duplicated()])].sort_values("title")
repeated
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>release_date</th>
    </tr>
    <tr>
      <th>movie_id</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>670</th>
      <td>Body Snatchers</td>
      <td>1993-01-01</td>
    </tr>
    <tr>
      <th>573</th>
      <td>Body Snatchers</td>
      <td>1993-01-01</td>
    </tr>
    <tr>
      <th>1645</th>
      <td>Butcher Boy, The</td>
      <td>1998-01-01</td>
    </tr>
    <tr>
      <th>1650</th>
      <td>Butcher Boy, The</td>
      <td>1998-01-01</td>
    </tr>
    <tr>
      <th>218</th>
      <td>Cape Fear</td>
      <td>1991-01-01</td>
    </tr>
    <tr>
      <th>673</th>
      <td>Cape Fear</td>
      <td>1962-01-01</td>
    </tr>
    <tr>
      <th>1234</th>
      <td>Chairman of the Board</td>
      <td>1998-01-01</td>
    </tr>
    <tr>
      <th>1654</th>
      <td>Chairman of the Board</td>
      <td>1998-01-01</td>
    </tr>
    <tr>
      <th>246</th>
      <td>Chasing Amy</td>
      <td>1997-01-01</td>
    </tr>
    <tr>
      <th>268</th>
      <td>Chasing Amy</td>
      <td>1997-01-01</td>
    </tr>
    <tr>
      <th>999</th>
      <td>Clean Slate</td>
      <td>1994-01-01</td>
    </tr>
    <tr>
      <th>1560</th>
      <td>Clean Slate</td>
      <td>1981-01-01</td>
    </tr>
    <tr>
      <th>309</th>
      <td>Deceiver</td>
      <td>1997-01-01</td>
    </tr>
    <tr>
      <th>1606</th>
      <td>Deceiver</td>
      <td>1997-01-01</td>
    </tr>
    <tr>
      <th>1256</th>
      <td>Designated Mourner, The</td>
      <td>1997-05-23</td>
    </tr>
    <tr>
      <th>1257</th>
      <td>Designated Mourner, The</td>
      <td>1997-05-23</td>
    </tr>
    <tr>
      <th>329</th>
      <td>Desperate Measures</td>
      <td>1998-01-30</td>
    </tr>
    <tr>
      <th>348</th>
      <td>Desperate Measures</td>
      <td>1998-01-30</td>
    </tr>
    <tr>
      <th>304</th>
      <td>Fly Away Home</td>
      <td>1996-09-13</td>
    </tr>
    <tr>
      <th>500</th>
      <td>Fly Away Home</td>
      <td>1996-09-13</td>
    </tr>
    <tr>
      <th>1617</th>
      <td>Hugo Pool</td>
      <td>1997-01-01</td>
    </tr>
    <tr>
      <th>1175</th>
      <td>Hugo Pool</td>
      <td>1997-01-01</td>
    </tr>
    <tr>
      <th>1395</th>
      <td>Hurricane Streets</td>
      <td>1998-01-01</td>
    </tr>
    <tr>
      <th>1607</th>
      <td>Hurricane Streets</td>
      <td>1998-01-01</td>
    </tr>
    <tr>
      <th>305</th>
      <td>Ice Storm, The</td>
      <td>1997-01-01</td>
    </tr>
    <tr>
      <th>865</th>
      <td>Ice Storm, The</td>
      <td>1997-01-01</td>
    </tr>
    <tr>
      <th>680</th>
      <td>Kull the Conqueror</td>
      <td>1997-08-29</td>
    </tr>
    <tr>
      <th>266</th>
      <td>Kull the Conqueror</td>
      <td>1997-08-29</td>
    </tr>
    <tr>
      <th>881</th>
      <td>Money Talks</td>
      <td>1997-08-22</td>
    </tr>
    <tr>
      <th>876</th>
      <td>Money Talks</td>
      <td>1997-08-22</td>
    </tr>
    <tr>
      <th>1625</th>
      <td>Nightwatch</td>
      <td>1997-04-22</td>
    </tr>
    <tr>
      <th>1477</th>
      <td>Nightwatch</td>
      <td>1997-04-22</td>
    </tr>
    <tr>
      <th>274</th>
      <td>Sabrina</td>
      <td>1995-01-01</td>
    </tr>
    <tr>
      <th>486</th>
      <td>Sabrina</td>
      <td>1954-01-01</td>
    </tr>
    <tr>
      <th>1442</th>
      <td>Scarlet Letter, The</td>
      <td>1995-01-01</td>
    </tr>
    <tr>
      <th>1542</th>
      <td>Scarlet Letter, The</td>
      <td>1926-01-01</td>
    </tr>
    <tr>
      <th>1286</th>
      <td>Shall We Dance?</td>
      <td>1937-01-01</td>
    </tr>
    <tr>
      <th>251</th>
      <td>Shall We Dance?</td>
      <td>1997-07-11</td>
    </tr>
    <tr>
      <th>1680</th>
      <td>Sliding Doors</td>
      <td>1998-01-01</td>
    </tr>
    <tr>
      <th>1429</th>
      <td>Sliding Doors</td>
      <td>1998-01-01</td>
    </tr>
    <tr>
      <th>711</th>
      <td>Substance of Fire, The</td>
      <td>1996-12-06</td>
    </tr>
    <tr>
      <th>1658</th>
      <td>Substance of Fire, The</td>
      <td>1996-12-06</td>
    </tr>
    <tr>
      <th>1003</th>
      <td>That Darn Cat!</td>
      <td>1997-02-14</td>
    </tr>
    <tr>
      <th>1444</th>
      <td>That Darn Cat!</td>
      <td>1965-01-01</td>
    </tr>
    <tr>
      <th>878</th>
      <td>That Darn Cat!</td>
      <td>1997-02-14</td>
    </tr>
    <tr>
      <th>303</th>
      <td>Ulee's Gold</td>
      <td>1997-01-01</td>
    </tr>
    <tr>
      <th>297</th>
      <td>Ulee's Gold</td>
      <td>1997-01-01</td>
    </tr>
  </tbody>
</table>
</div>



### Of the repeated titles, which are duplication errors?


```python
dupes = repeated.groupby(['title', 'release_date']).size().reset_index()
dupes.columns=['title','release_date','dupe_count']
errors = dupes.title[dupes.dupe_count>1]
errors
```




    0              Body Snatchers 
    1            Butcher Boy, The 
    4       Chairman of the Board 
    5                 Chasing Amy 
    8                    Deceiver 
    9     Designated Mourner, The 
    10         Desperate Measures 
    11              Fly Away Home 
    12                  Hugo Pool 
    13          Hurricane Streets 
    14             Ice Storm, The 
    15         Kull the Conqueror 
    16                Money Talks 
    17                 Nightwatch 
    24              Sliding Doors 
    25     Substance of Fire, The 
    27             That Darn Cat! 
    28                Ulee's Gold 
    Name: title, dtype: object



### Which are remakes? 


```python
remakes = dupes.title[dupes.dupe_count<2].drop_duplicates()
remakes
```




    2               Cape Fear 
    6             Clean Slate 
    18                Sabrina 
    20    Scarlet Letter, The 
    22        Shall We Dance? 
    26         That Darn Cat! 
    Name: title, dtype: object



### How many movies were released in December?


```python
df['year'] = pd.DatetimeIndex(df['release_date']).year.astype(int)
df['month'] = pd.DatetimeIndex(df['release_date']).month.astype(int)
df['day'] = pd.DatetimeIndex(df['release_date']).day.astype(int)
len(df[df.month==12])
```




    38



### Which movies have an animal in the title?


```python
df['title'] = df['title'].str.lower()
animals = ['dog', 'cat', 'fish', 'monkey', 'elephant', 'tiger', 'lion', 'hamster', 'pig', 'insect', 'bird']
pattern = '|'.join(animals)
df[df.title.str.contains(pattern)]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>release_date</th>
      <th>year</th>
      <th>month</th>
      <th>day</th>
    </tr>
    <tr>
      <th>movie_id</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>copycat</td>
      <td>1995-01-01</td>
      <td>1995</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>twelve monkeys</td>
      <td>1995-01-01</td>
      <td>1995</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>20</th>
      <td>angels and insects</td>
      <td>1995-01-01</td>
      <td>1995</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>25</th>
      <td>birdcage, the</td>
      <td>1996-03-08</td>
      <td>1996</td>
      <td>3</td>
      <td>8</td>
    </tr>
    <tr>
      <th>71</th>
      <td>lion king, the</td>
      <td>1994-01-01</td>
      <td>1994</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>74</th>
      <td>faster pussycat! kill! kill!</td>
      <td>1965-01-01</td>
      <td>1965</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>102</th>
      <td>aristocats, the</td>
      <td>1970-01-01</td>
      <td>1970</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>103</th>
      <td>all dogs go to heaven 2</td>
      <td>1996-03-29</td>
      <td>1996</td>
      <td>3</td>
      <td>29</td>
    </tr>
    <tr>
      <th>111</th>
      <td>truth about cats &amp; dogs, the</td>
      <td>1996-04-26</td>
      <td>1996</td>
      <td>4</td>
      <td>26</td>
    </tr>
    <tr>
      <th>153</th>
      <td>fish called wanda, a</td>
      <td>1988-01-01</td>
      <td>1988</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>156</th>
      <td>reservoir dogs</td>
      <td>1992-01-01</td>
      <td>1992</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>171</th>
      <td>delicatessen</td>
      <td>1991-01-01</td>
      <td>1991</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>256</th>
      <td>when the cats away</td>
      <td>1997-06-20</td>
      <td>1997</td>
      <td>6</td>
      <td>20</td>
    </tr>
    <tr>
      <th>307</th>
      <td>devil's advocate, the</td>
      <td>1997-01-01</td>
      <td>1997</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>347</th>
      <td>wag the dog</td>
      <td>1998-01-09</td>
      <td>1998</td>
      <td>1</td>
      <td>9</td>
    </tr>
    <tr>
      <th>427</th>
      <td>to kill a mockingbird</td>
      <td>1962-01-01</td>
      <td>1962</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>443</th>
      <td>birds, the</td>
      <td>1963-01-01</td>
      <td>1963</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>490</th>
      <td>to catch a thief</td>
      <td>1955-01-01</td>
      <td>1955</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>499</th>
      <td>cat on a hot tin roof</td>
      <td>1958-01-01</td>
      <td>1958</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>529</th>
      <td>my life as a dog</td>
      <td>1985-01-01</td>
      <td>1985</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>587</th>
      <td>hour of the pig, the</td>
      <td>1993-01-01</td>
      <td>1993</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>674</th>
      <td>cat people</td>
      <td>1982-01-01</td>
      <td>1982</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>733</th>
      <td>go fish</td>
      <td>1994-01-01</td>
      <td>1994</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>843</th>
      <td>shaggy dog, the</td>
      <td>1959-01-01</td>
      <td>1959</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>871</th>
      <td>vegas vacation</td>
      <td>1997-02-14</td>
      <td>1997</td>
      <td>2</td>
      <td>14</td>
    </tr>
    <tr>
      <th>878</th>
      <td>that darn cat!</td>
      <td>1997-02-14</td>
      <td>1997</td>
      <td>2</td>
      <td>14</td>
    </tr>
    <tr>
      <th>972</th>
      <td>passion fish</td>
      <td>1992-01-01</td>
      <td>1992</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>989</th>
      <td>cats don't dance</td>
      <td>1997-03-26</td>
      <td>1997</td>
      <td>3</td>
      <td>26</td>
    </tr>
    <tr>
      <th>1003</th>
      <td>that darn cat!</td>
      <td>1997-02-14</td>
      <td>1997</td>
      <td>2</td>
      <td>14</td>
    </tr>
    <tr>
      <th>1170</th>
      <td>spanking the monkey</td>
      <td>1994-01-01</td>
      <td>1994</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1254</th>
      <td>gone fishin'</td>
      <td>1997-05-30</td>
      <td>1997</td>
      <td>5</td>
      <td>30</td>
    </tr>
    <tr>
      <th>1318</th>
      <td>catwalk</td>
      <td>1996-06-07</td>
      <td>1996</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1364</th>
      <td>bird of prey</td>
      <td>1996-10-04</td>
      <td>1996</td>
      <td>10</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1379</th>
      <td>love and other catastrophes</td>
      <td>1997-03-28</td>
      <td>1997</td>
      <td>3</td>
      <td>28</td>
    </tr>
    <tr>
      <th>1434</th>
      <td>shooting fish</td>
      <td>1998-01-16</td>
      <td>1998</td>
      <td>1</td>
      <td>16</td>
    </tr>
    <tr>
      <th>1444</th>
      <td>that darn cat!</td>
      <td>1965-01-01</td>
      <td>1965</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1445</th>
      <td>ladybird ladybird</td>
      <td>1994-01-01</td>
      <td>1994</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1510</th>
      <td>mad dog time</td>
      <td>1996-11-08</td>
      <td>1996</td>
      <td>11</td>
      <td>8</td>
    </tr>
    <tr>
      <th>1514</th>
      <td>dream with the fishes</td>
      <td>1997-06-20</td>
      <td>1997</td>
      <td>6</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1531</th>
      <td>far from home: the adventures of yellow dog</td>
      <td>1995-01-01</td>
      <td>1995</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1679</th>
      <td>b. monkey</td>
      <td>1998-02-06</td>
      <td>1998</td>
      <td>2</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>



### Which movies have a title longer than 10 words?


```python
df['words'] = df['title'].str.split()
```


```python
for index, row in df.iterrows():
    df['words'][index] = len(df['words'][index])
```

    /Users/pepper/anaconda/envs/ytestpc/lib/python3.5/site-packages/ipykernel/__main__.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      from ipykernel import kernelapp as app



```python
df[df['words']>10]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>release_date</th>
      <th>year</th>
      <th>month</th>
      <th>day</th>
      <th>words</th>
    </tr>
    <tr>
      <th>movie_id</th>
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
      <th>474</th>
      <td>dr. strangelove or: how i learned to stop worr...</td>
      <td>1963-01-01</td>
      <td>1963</td>
      <td>1</td>
      <td>1</td>
      <td>13</td>
    </tr>
    <tr>
      <th>580</th>
      <td>englishman who went up a hill, but came down a...</td>
      <td>1995-01-01</td>
      <td>1995</td>
      <td>1</td>
      <td>1</td>
      <td>12</td>
    </tr>
    <tr>
      <th>1059</th>
      <td>don't be a menace to south central while drink...</td>
      <td>1996-01-01</td>
      <td>1996</td>
      <td>1</td>
      <td>1</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
