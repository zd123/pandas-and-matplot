## Overview
Okay, so y’all have heard of Moneyball, if not, get out from under the rock where you are living and see the movie, better yet read the book by michael lewis.

Regardless, it doesn’t really matter… all you really need to know is that they found a new and better statistic for producing wins.  Instead of using the normal stats traditionally used in sabermetrics (the stats you see on the back of every baseball card), they created new stats based on the old stats that were better indicators of winning games, and more cost effective (ie undervalued in terms of player salary)

(If you dont have the baseball-csvs.zip get it here http://seanlahman.com/files/database/lahman-csv_2014-02-14.zip ).  I've renamed it baseball-csvs cause its easier to type.  Unzip the baseball-csvs.zip file, move the unzipped baseball-csvs folder inside the data folder.

# MAIN GOAL: Find which offensive stat contributes most to winning games.  

### PART 0
__Main goal for Part 0:__ Create a dataframe of each teams  batting statistics for each year. This dataframe should also include each teams Wins, Losses, and Rank for each year.  This data frame will **only include the years from 1980 – 2010.  **   <br>
Inspect the csv files.  Read the readme2013.txt.  Since we want to find how batting stats have impacted team wins, which files are we going to use, and how are we going to join/merge them?
(Answer is to use the Batting.csv and Teams.csv )
1.  Build a data frame that looks like this:
##### EXPECTED RESULTS:
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>yearID</th>
      <th>teamID</th>
      <th>G</th>
      <th>W</th>
      <th>L</th>
      <th>Rank</th>
      <th>AB</th>
      <th>R</th>
      <th>H</th>
      <th>2B</th>
      <th>3B</th>
      <th>HR</th>
      <th>RBI</th>
      <th>SB</th>
      <th>CS</th>
      <th>BB</th>
      <th>SO</th>
      <th>SF</th>
      <th>HBP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td> 1980</td>
      <td> NYA</td>
      <td> 162</td>
      <td> 103</td>
      <td> 59</td>
      <td> 1</td>
      <td> 5553</td>
      <td> 820</td>
      <td> 1484</td>
      <td> 239</td>
      <td> 34</td>
      <td> 189</td>
      <td> 772</td>
      <td>  86</td>
      <td> 36</td>
      <td> 643</td>
      <td> 739</td>
      <td> 54</td>
      <td> 28</td>
    </tr>
    <tr>
      <th>1</th>
      <td> 1980</td>
      <td> BAL</td>
      <td> 162</td>
      <td> 100</td>
      <td> 62</td>
      <td> 2</td>
      <td> 5585</td>
      <td> 805</td>
      <td> 1523</td>
      <td> 258</td>
      <td> 29</td>
      <td> 156</td>
      <td> 751</td>
      <td> 111</td>
      <td> 38</td>
      <td> 587</td>
      <td> 766</td>
      <td> 46</td>
      <td> 21</td>
    </tr>
    <tr>
      <th>2</th>
      <td> 1980</td>
      <td> ML4</td>
      <td> 162</td>
      <td>  86</td>
      <td> 76</td>
      <td> 3</td>
      <td> 5653</td>
      <td> 811</td>
      <td> 1555</td>
      <td> 298</td>
      <td> 36</td>
      <td> 203</td>
      <td> 774</td>
      <td> 131</td>
      <td> 56</td>
      <td> 455</td>
      <td> 745</td>
      <td> 51</td>
      <td> 25</td>
    </tr>
    <tr>
      <th>3</th>
      <td> 1980</td>
      <td> DET</td>
      <td> 163</td>
      <td>  84</td>
      <td> 78</td>
      <td> 4</td>
      <td> 5648</td>
      <td> 830</td>
      <td> 1543</td>
      <td> 232</td>
      <td> 53</td>
      <td> 143</td>
      <td> 767</td>
      <td>  75</td>
      <td> 68</td>
      <td> 645</td>
      <td> 844</td>
      <td> 55</td>
      <td> 33</td>
    </tr>
    <tr>
      <th>4</th>
      <td> 1980</td>
      <td> BOS</td>
      <td> 160</td>
      <td>  83</td>
      <td> 77</td>
      <td> 5</td>
      <td> 5603</td>
      <td> 757</td>
      <td> 1588</td>
      <td> 297</td>
      <td> 36</td>
      <td> 162</td>
      <td> 717</td>
      <td>  79</td>
      <td> 48</td>
      <td> 475</td>
      <td> 720</td>
      <td> 50</td>
      <td> 32</td>
    </tr>
  </tbody>
</table>

---
### PART 1
Engineer the following features for each team for each year.
1. Batting Average  (total  HITS / total AT BATS)
2. On Base Percentage (OBP)  http://en.wikipedia.org/wiki/On-base_percentage
4. Slugging Percentage (SLG) http://en.wikipedia.org/wiki/Slugging_percentage
5. ** OPTIONAL** Weight On Base Average (wOBA)  http://en.wikipedia.org/wiki/WOBA

##### EXPECTED RESULTS:
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>yearID</th>
      <th>teamID</th>
      <th>G</th>
      <th>W</th>
      <th>L</th>
      <th>Rank</th>
      <th>AB</th>
      <th>R</th>
      <th>H</th>
      <th>2B</th>
      <th>3B</th>
      <th>HR</th>
      <th>RBI</th>
      <th>SB</th>
      <th>CS</th>
      <th>BB</th>
      <th>SO</th>
      <th>SF</th>
      <th>HBP</th>
      <th>BA</th>
      <th>OBP</th>
      <th>1B</th>
      <th>SLG</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td> 1980</td>
      <td> NYA</td>
      <td> 162</td>
      <td> 103</td>
      <td> 59</td>
      <td> 1</td>
      <td> 5553</td>
      <td> 820</td>
      <td> 1484</td>
      <td> 239</td>
      <td> 34</td>
      <td> 189</td>
      <td> 772</td>
      <td>  86</td>
      <td> 36</td>
      <td> 643</td>
      <td> 739</td>
      <td> 54</td>
      <td> 28</td>
      <td> 0.267243</td>
      <td> 0.343262</td>
      <td> 1022</td>
      <td> 0.424635</td>
    </tr>
    <tr>
      <th>1</th>
      <td> 1980</td>
      <td> BAL</td>
      <td> 162</td>
      <td> 100</td>
      <td> 62</td>
      <td> 2</td>
      <td> 5585</td>
      <td> 805</td>
      <td> 1523</td>
      <td> 258</td>
      <td> 29</td>
      <td> 156</td>
      <td> 751</td>
      <td> 111</td>
      <td> 38</td>
      <td> 587</td>
      <td> 766</td>
      <td> 46</td>
      <td> 21</td>
      <td> 0.272695</td>
      <td> 0.341561</td>
      <td> 1080</td>
      <td> 0.413071</td>
    </tr>
    <tr>
      <th>2</th>
      <td> 1980</td>
      <td> ML4</td>
      <td> 162</td>
      <td>  86</td>
      <td> 76</td>
      <td> 3</td>
      <td> 5653</td>
      <td> 811</td>
      <td> 1555</td>
      <td> 298</td>
      <td> 36</td>
      <td> 203</td>
      <td> 774</td>
      <td> 131</td>
      <td> 56</td>
      <td> 455</td>
      <td> 745</td>
      <td> 51</td>
      <td> 25</td>
      <td> 0.275075</td>
      <td> 0.329075</td>
      <td> 1018</td>
      <td> 0.448258</td>
    </tr>
    <tr>
      <th>3</th>
      <td> 1980</td>
      <td> DET</td>
      <td> 163</td>
      <td>  84</td>
      <td> 78</td>
      <td> 4</td>
      <td> 5648</td>
      <td> 830</td>
      <td> 1543</td>
      <td> 232</td>
      <td> 53</td>
      <td> 143</td>
      <td> 767</td>
      <td>  75</td>
      <td> 68</td>
      <td> 645</td>
      <td> 844</td>
      <td> 55</td>
      <td> 33</td>
      <td> 0.273194</td>
      <td> 0.348065</td>
      <td> 1115</td>
      <td> 0.408994</td>
    </tr>
    <tr>
      <th>4</th>
      <td> 1980</td>
      <td> BOS</td>
      <td> 160</td>
      <td>  83</td>
      <td> 77</td>
      <td> 5</td>
      <td> 5603</td>
      <td> 757</td>
      <td> 1588</td>
      <td> 297</td>
      <td> 36</td>
      <td> 162</td>
      <td> 717</td>
      <td>  79</td>
      <td> 48</td>
      <td> 475</td>
      <td> 720</td>
      <td> 50</td>
      <td> 32</td>
      <td> 0.283420</td>
      <td> 0.340097</td>
      <td> 1093</td>
      <td> 0.436016</td>
    </tr>
  </tbody>
</table>

### PART 2
This is where you are going to get down and dirty with joins and merges and aggregates and pandas in general.  Hopefully by the end of this you will all have your pandas paws.
1.  Find which batting statistic contributes most to a team winning

# YO THIS IS WHERE I NEED TO FIGURE OUT THE BEST WAY TO DO THIS


### PART 3
Now it is time to see the effect (affect?) Moneyball has had on players salaries since it became popular.  You will need to find which table the salary information is in, and how to join it with the batting data.
1.  Find if the average salary of players with high, med, and low OBP.
2.  Create a line graph for each of these groups where the x-axis is time, and the y-axis is salary.  Each group should be a different colored line all on the same graph.  

---
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
