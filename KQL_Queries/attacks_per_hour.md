#Attacks per hour


```
CowrieDCR_CL
| summarize Attacks = count() by bin(TimeGenerated, 1h)
| sort by TimeGenerated desc
```

## Query Breakdown
- Table name at top, this is the table being queried
- summarize Attacks = count() : the attacks are rounded to the hour, then it collects a count of it
- by bin(TimeGenerated, 1h) : As Cowrie records the timestamps down to the nearest second, I can round it to the nearest hour to help create a graph.
- sort by TimeGenerated desc: sort by most recent attacks first 

