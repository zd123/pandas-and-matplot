## Overview

_Based on a true events_

You are a rouge data scientist living in South Brooklyn. The streets are bad enough, but what is worse is the health conditions of the projects. Your neighbor, who introduced himself as Franklin, has been missing for the last week. Upon his return, he tells you he's been in the hospital for "Viral Meningitis".
That's when his brother, Bundles, beings showing symptoms of "Viral Meningitis".

He only has __xxxxx__ money he can spend, and he asks you to help him find the best hospital to go to for the least amount of cash money.

## Goals
* pandas file loading
* pandas aggregates
* pandas plotting

## Assignment

The first goal of this sprint is to find which hospital costs, and charges the most for treating "Viral Meningitis". In addition which hospital treats the most patients with VM.

1. Read the data set into pandas and familiarize yourself with the set you will be working with.
2. To just do some basic exploratory analysis, compute the most common cause of hospitalization (affliction)
    * Compare the execution time of using `value_counts()` vs. counting with `groupby()`
2. Keep the official pandas documentation to apply generously as needed. [http://pandas.pydata.org/pandas-docs/stable/](http://pandas.pydata.org/pandas-docs/stable/)

### Count that CASH

The amount in the charge/costs columns is the price per discharge. Most hospitals treat many people with the same illness.  The number they treat is the number in the "Discharges" column.

#### It is your job to calculate all the totals.

1. Create a new column that is the __Discharges__ __x__ __Mean Charge__.  Then do the same for the "Mean Cost".
2. With theses two new __Total Charges__ and __Total Costs__ columns, calculate the Markup for each row.
3. Tell me which procedure has the highest markup, and which one has the lowest markup

#### Expected Results:

__Lowest__

| Facility Name | ... | Total Charge | Total Cost | Markup|
| ------------- |---|:-------------:| -----:|------|
|TLC Health Network Tri-County Memorial Hospital | ...|  1540540    | 97482510  | 0.015803|

__Highest__

| Facility Name | ... | Total Charge | Total Cost | Markup|
| ------------- |---|:-------------:| -----:|------|
| SUNY Downstate Medical Center at LICH | ... | 43088   | 2068  | 20.835590|

### Find that MONEY
Now we want to see which hospital has the most $$$ coming.
To keep this from getting messy, lets create a new DataFrame with only the columns we care about.

1.  Create a new DataFrame named "net" that is only the Hospital Name, Total Charge, Total Cost from our original DataFrame
1.  Find the total amount much each hospital spent, and how much they charged. (Group your data by Facility names, and sum all the total costs and total charges)
1.  Now find the net income for every hospital. Tell me the most profitable and the least profitable ones and how much they is making (billions trillionz?)

#### Expected Results:

| Facility Name|Total Charge|Total Cost|Net Income|
|----|----|----|----|
| Adirondack Medical Center-Saranac Lake Site|141573499.0|77427664.0|64145835.0 |
| Albany Medical Center - South Clinical Campus|1802808.0|1432784.0|370024.0 |
| Albany Medical Center Hospital|3763945310.0|1336298908.0|2427646402.0 |
| Albany Memorial Hospital|221974029.0|94907174.0|127066855.0 |
|...|...|...|...|



## FIND MOST POPULAR SICKNESS
I included this question to be tricky on purpose.  Notice the **APR DRG Description** should be unique for each hospital, however, hospitals also have a label for how severe that illness is.  So each illness can be listed up to four times. they are separated and labeled accordingly with the **APR Severity of Illness Description**.  This is annoying because it just is.  Start by Group all the levels of severity for each Illness...

### 1. Which illness has the most discharges?

#### Expected Results:
|  | Discharges | Total Charge | Total Cost |
| ------------- |---|:-------------:| -----:|------|
|APR DRG Description  | | | |
|Neonate Birthwt >2499G, Normal Newborn Or Neonate W Other Problem | 632412 | 2956415168 | 1168223473 |



---
### 1. What is the most expensive type of illness?

#### Expected Results:
|  | Discharges | Total Charge | Total Cost |
| ------------- |---|:-------------:| -----:|------|
|APR DRG Description  | | | |
|Septicemia & Disseminated Infections | 161739 | 8182068670 | 3180766286 |

<BR>



#### Now, lets focus in on "Viral Meningitis"

1. Create a new dataframe that only contains the data corresponding to "Viral Meningitis"

```python
newdf = df[df["Illness"] == "Viral Meningitis"]]
```

2. Now, with our newdf, only keep the data columns we care about which are:

```python
["Facility Name", "APR DRG Description","Discharges", "Mean Charge", "Median Charge", "Mean Cost"]
```

#### Our newdf should look somewhat like this:

|Facility Name|APR DRG Description|APR Severity of Illness Description|Discharges|Mean Charge|Median Charge|Mean Cost|
|----|----|----|----|----|----|----|
|Adirondack Medical Center-Saranac Lake Site|Viral Meningitis|Minor|1|17116.0|17116.0|7006.0|
|Albany Medical Center Hospital|Viral Meningitis|Minor|19|13212.0|11914.0|4569.0|
|Albany Medical Center Hospital|Viral Meningitis|Moderate|11|21197.0|14197.0|7131.0|
|Albany Medical Center Hospital|Viral Meningitis|Major|6|28074.0|22846.0|7495.0|

---


### 1. Find which hospital has the most cases of Viral Meningitis.

#### Expected Results:

| Facility Name | ... | Discharges |
| ------------- |-----|:----------:|
| North Shore University Hospital | ... | 158 |
| Montefiore Medical Center - Henry & Lucy Moses Div | ... | 152 |
| Strong Memorial Hospital | ... | 117 |

1. Find which hospital is the least expensive for treating Moderate cases of VM. **note example below is the most expensive not the least**

|Facility Name|APR DRG Description|APR Severity of Illness Description|Discharges|Mean Charge|Median Charge|Mean Cost |
|---|---|---|---|---|---|---|
|Beth Israel Med Center-Kings Hwy Div|Viral Meningitis|Moderate|1|71663.0|71663.0|12658.0|
|Lutheran Medical Center|Viral Meningitis|Moderate|2|71850.0|71850.0|50605.0|
|New York Presbyterian Hospital - Downtown Division|Viral Meningitis|Moderate|1|76528.0|76528.0|27563.0|
|St Lukes Roosevelt Hospital - St Lukes Hospital Division|Viral Meningitis|Moderate|4|79245.0|48006.0|24743.0|
|Orange Regional Medical Center|Viral Meningitis|Moderate|1|84003.0|84003.0|23143.0|

4. Find which hospital is the least expensive for treating Moderate cases of VM **that have at least 3 or more Discarges**.

|Facility Name|APR DRG Description|APR Severity of Illness Description|Discharges|Mean Charge|Median Charge|Mean Cost
|----|----|----|----|----|---|----|
|Cayuga Medical Center at Ithaca|Viral Meningitis|Moderate|6|5738.0|5111.0|3949.0
|Women And Children's Hospital Of Buffalo|Viral Meningitis|Moderate|31|6601.0|6182.0|2770.0|
|Millard Fillmore Suburban Hospital|Viral Meningitis|Moderate|6|6614.0|6784.0|2649.0|

5. Find if there is a correlation between severity of illness and how much much is charged. Hint use df.corr() *http://pandas.pydata.org/pandas-docs/stable/computation.html#correlation*

|| Discharges |	Mean Charge |
|----|----| ---|
|Discharges | 1.000000	| 0.925377 |
|Mean Charge |	 0.925377	| 1.000000 |


### IF YOU ARE FINISHED WITH THIS EXERCISE, GO ON TO ADVANCED PANDAS WITH BASEBALL DATA **

## References

* Python for Data Analysis: Chapter 5, 8, 9
* [pandas homepage](http://pandas.pydata.org/)
* [pandas documentation](http://pandas.pydata.org/pandas-docs/stable/index.html)
* [pandas tutorial](http://www.randalolson.com/2012/08/06/statistical-analysis-made-easy-in-python/)
* [pandas: Merge, Join, and Concatenate](http://pandas.pydata.org/pandas-docs/stable/merging.html)
* [pandas: Selecting Data](http://pandas.pydata.org/pandas-docs/stable/indexing.html)
* [pandas Group By: split-apply-combine](http://pandas.pydata.org/pandas-docs/stable/groupby.html)
* [pandas `apply`](http://pandas.pydata.org/pandas-docs/stable/groupby.html#flexible-apply)
* [pandas `sort_index`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.sort_index.html#pandas.DataFrame.sort_index)
* [pandas `head`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.head.html#pandas.DataFrame.head)
