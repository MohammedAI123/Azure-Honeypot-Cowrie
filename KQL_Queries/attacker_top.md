# Attacker Top IPs

```
CowrieDCR_CL
| extend ClientIP = extract(@"(\d{1,3}\.){3}\d{1,3}", 0, message)
| where isnotempty(ClientIP)

| where ClientIP !startswith "10."
      and ClientIP !startswith "192.168."
      and ClientIP !startswith "172."
      and ClientIP !startswith "127."
| summarize Attempts = count() by ClientIP
| sort by Attempts desc
| take 20
```

**This KQL query obtains the attacker IPs and collects a count of how many times each IP address appears**

## Query Breakdown
- starts with the table name, this is the area where the query is being applied to
- extend clientIP: creates a new column called ClientIP
- extract : this function is used to find text, and extract the IP address directly from the logs, since the cowrie logs shows a new connection like this; **New connection: 139.199.80.137:51790 (x.x.x.x)** I had to extract the IP out of the text
--\d{1,3} - 1-3 digits
--{3} - this repeats the previous sequence 3 times
--\d{1,3} - then the final group of digits
--in total it covers the format of an IPv4 address, e.g. 234.148.12.34, 121.33.456.34
  
- where isnotempty(ClientIP) - filtering out logs that dont match an IP, as it isnt needed for this query
- and ClientIP !startswith "xxx.xxx" - excluding IP ranges that cover an internal IP, as this isnt an attacker
- summarize attempts = count() by ClientIP - groups the results and makes a count of it
- sort by Attempts desc - sorts them in descedning order, biggest to smallest
- take 20 - takes the 20 most common IPs, can change to any number
- once complete and results are shown, we can change the visualisation type and time range. As an example, ive chosen a bar chart that show sresults over he last 30 days


