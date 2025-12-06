# Attacker Top IPs

```
CowrieDCR_CL
| extend AttackerIP = extract(@"(\d{1,3}\.){3}\d{1,3}", 0, message)
| where isnotempty(AttackerIP)

| where AttackerIP !startswith "10."
      and AttackerIP !startswith "192.168."
      and AttackerIP !startswith "172."
      and AttackerIP !startswith "127."
| summarize Attempts = count() by AttackerIP
| sort by Attempts desc
| take 20
```

**This KQL query obtains the attacker IPs and collects a count of how many times each IP address appears, starting with the most common first**

## Query Breakdown
- Table name at top, this is the area being queried
- extend AttackerIP: creates a new column called AttackerIP
- extractextract(@"(\d{1,3}\.){3}\d{1,3}", 0, message) : this function is used to find text, and extract the IP address directly from the logs, since the cowrie logs shows a new connection like this; **New connection: 139.199.80.137:51790 (x.x.x.x)** I had to extract the IP out of the text only
  1. \d{1,3} - 1-3 digits
  2. {3} - this repeats the previous sequence 3 times
  3. \d{1,3} - then the final group of digits
  4.  in total it covers the format of an IPv4 address, e.g. 234.148.12.34, 121.33.456.34
  
- where isnotempty(AttackerIP) -       filtering out logs that dont match an IP, as it isnt needed for this query
- and AttackerIP !startswith "xxx.xxx" -       excluding IP ranges that cover an internal IP, as this isnt an attacker IP
- summarize attempts = count() by AttackerIP -       groups the results and makes a count of it
- sort by Attempts desc -       sorts them in descending order, biggest to smallest
- take 20 -       takes the 20 most common IPs, can be change to any number 
- once complete and results are shown, we can change the visualisation type and time range. As an example, I have chosen a bar chart that shows results over the last 30 days


