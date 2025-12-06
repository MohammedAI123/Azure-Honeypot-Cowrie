# Login Attempts

```
CowrieDCR_CL
| where message has_any ("login", "success", "command")
| project TimeGenerated, message
| sort by TimeGenerated desc
| take 100
```
**This query filters out the cowrie logs to find login attempts that were successful and unsuccessful, as well as commands attempted by attackers. It also shows a timestamp of when the attack occured**

## Query Breakdown
- Table name at top, this is the table thats being queried
- where message has_any ("login", "success", "command") : filters out the logs to just return rows that include login,success,command
- sort by TimeGenerated desc : This sorts the attacks in descending order, so the latest attacks show first
- project TimeGenerated, message : This selects the 2 columns I want, timestamp and the log message
- take 100 : takes 100 rows of results
- once complete, I can alter the time range and visualisation, I have chosen a grid view of attacks over the last 7 days.
