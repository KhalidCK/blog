---
title: "When to Go Out"
date: 2018-06-06T20:20:44+02:00
draft: true
---


Good weather is *almost* back and most people think to workout outside.

Seems like a good idea however air pollution can be problematic.

## What's the problem with air ?

Air pollution is a major issue since several decades, and there is a well known relationship between it and multiple health problem.

Practicing a physical activities can make you more exposed to pollution according to several sources

>you usually inhale more air and breathe it more deeply into your lungs. And because you're more likely to breathe deeply through your mouth during exercise, the air you breathe in generally bypasses your nasal passages, which normally filter airborne pollution particles.

[ref](https://www.mayoclinic.org/healthy-lifestyle/fitness/expert-answers/air-pollution-and-exercise/faq-20058563)

I'll try to find out when I'll be least expose in my distriction (13eme) in Paris

For that I've downloaded a timeseries dataset provided [airparif](www.airparif.assos.fr)

It contains information about two main polluant NO2 and O3 from 2009 to march 2018

Load data

```python
#some helper to ease manipulation
from utils import read_air,save_img
```


```python
df = read_air('data/20090101_20180301-PA13_auto.csv').set_index('date')
```

```python
df.head()
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
      <th>NO2</th>
      <th>O3</th>
    </tr>
    <tr>
      <th>date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2009-01-01 01:00:00</th>
      <td>56.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2009-01-01 02:00:00</th>
      <td>57.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2009-01-01 03:00:00</th>
      <td>54.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2009-01-01 04:00:00</th>
      <td>60.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2009-01-01 05:00:00</th>
      <td>66.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



A quick look at data seems to indicate that during the whole year at some point, if you're over exposed to one of them


```python
ax= df.resample('1m').median().plot(figsize=(12,7),
                                    title='Monthly median')
ax.set_ylabel(unit)
```


![png](/img/air_quality/monthly-median.png)


Let's zoom on 2017


```python
year=2017
ax= df[str(year)].resample('1m').median().plot(figsize=(12,7),
                                               title=f'Monthly median for {year}',
                                               marker='o')
_=ax.set_ylabel(unit)
_=ax.set_ylim(bottom=0)
_=save_img('Monthly median for 2017')
```


![png](/img/air_quality/monthly-median-for-2017.png)


Ok, what is happening on average in June ?


```python
mask=df.index.month==6
agg = df[mask].index.hour
ax=df[mask].groupby(agg).median().plot(kind='bar',
                                       title='Hourly average in june',
                                       figsize=(15,7))
_=ax.set_ylabel(unit)
_=ax.set_xlabel('hour')

_=ax.set_ylim(bottom=0)
```


![png](/img/air_quality/hourly-average-in-june.png)


It looks like that my best bet is early in the morning before 9am
