# IPL_data_Analysis
IPL Matches Data Analysis Using Spark
***
### Columns name: <br> 
 id,season,city,date,team1,team2,toss_winner,toss_decision,result,dl_applied,winner,win_by_runs,win_by_wickets,player_of_match,venue,umpire1,umpire2,umpire3<br>
 ***
`Problem Statement 1: which stadium is best suited to bat first?`<br>
`Steps will be available soon`
<br><br>Finding the total number of matches played on each stadium<br>
```Scala
val data = sc.textFile("file:///home/Vishal/Documents/datasets/matches.csv")
 
val filtering_bad_records = data.map(line=>line.split(",")).filter(x=>x.length<19)
 
val extracting_columns = filtering_bad_records.map(x=>(x(7),x(11),x(12),x(14)))
 
val bat_first_won = extracting_columns.filter(x=>x._2!="0").map(x=>(x._4,1)) .reduceByKey(_+_).map(item => item.swap).sortByKey(false).collect.foreach(println)

```
