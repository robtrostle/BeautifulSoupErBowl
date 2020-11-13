#    Using pandas to scrape the ESPN SuperBowls Table

![](https://www.logopik.com/wp-content/uploads/edd/2018/06/Super-Bowl-50-logo-vector-free.png)

ESPN Site: http://www.espn.com/nfl/superbowl/history/winners


```python
import pandas as pd
```


```python
dfs = pd.read_html('http://www.espn.com/nfl/superbowl/history/winners')#reads into a list of dataFrames
```


```python
df = dfs[0]#Assign the lists to a DataFrame
winners = df.loc[2:]#skip the first 2 rows
champs = winners[3]#assign champs df to third column of the dataFrame
```


```python
df2 = winners[3].str.split(',').str[0]#split the string at the comma, keeping the left side of the string (winners + score)
```


```python
champList = list()#A list to hold the chemps
import re
for i in df2:#loop over df2
    clean = re.sub("(\s\d+)","",i).rstrip()#strip off the score and white spaces on the right
    champList.append(clean)#append the teams to the list
```


```python
team = str(input('Please pick a team (City Name Only) and I will tell you how many superbowls they won. \
If city has more than one team, include the mascot: (ex. New York Giants) '))#get team city
```

    Please pick a team (City Name Only) and I will tell you how many superbowls they won. If city has more than one team, include the mascot: (ex. New York Giants) Pittsburgh
    


```python
count = 0
if team in champList:
    for t in range(0,len(champList)):
        if team == champList[t]:
            count += 1
else:
    print("I don't know how to tell you this, but",team, "has not won any Super Bowls. Maybe next year?")
```


```python
print(team, "has won", count, "Super Bowl(s) ")
```

    Pittsburgh has won 6 Super Bowl(s) 
    


```python

```
