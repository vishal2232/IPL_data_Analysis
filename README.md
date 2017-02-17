# IPL_data_Analysis
IPL Matches Data Analysis Using Spark
***
### Columns name: <br> 
 id,season,city,date,team1,team2,toss_winner,toss_decision,result,dl_applied,winner,win_by_runs,win_by_wickets,player_of_match,venue,umpire1,umpire2,umpire3<br>
 ***
`Problem Statement 1: which stadium is best suited to bat first?`<br>

<br><br>Take out the columns toss_decision, won_by_runs, won_by_wickets and venue. <br>
```Scala
val data = sc.textFile("file:///home/Vishal/Documents/datasets/matches.csv")
 
val filtering_bad_records = data.map(line=>line.split(",")).filter(x=>x.length<19)
 
vals extracting_columns = filtering_bad_records.map(x=>(x(7),x(11),x(12),x(14)))
 
val bat_first_won = extracting_columns.filter(x=>x._2!="0").map(x=>(x._4,1)) .reduceByKey(_+_).map(item => item.swap).sortByKey(false).collect.foreach(println)

```
Now calculate the winning percentage of each stadium for first_bat_won.

```Scala
val join = bat_first_won.join(total_matches_per_venue).map(x=>(x._1,(x._2._1*100/x._2._2))).map(item => item.swap).sortByKey(false).collect.foreach(println)
```
