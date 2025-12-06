# Attack Map

```
CowrieDCR_CL
| extend AttackerIP = extract(@"(\d{1,3}\.){3}\d{1,3}", 0, message)
| where isnotempty(AttackerIP)
| extend Geo = geo_info_from_ip_address(AttackerIP)
| extend Country = tostring(Geo.country)
| summarize Attempts = count() by Country
| sort by Attempts desc
```
**This query uses Azure's built in geo location fucntions to take the IP addresses from Cowrie logs and match them to a country, after changing the format to a map, I can pinpoint where attacks originate from**

## Query Breakdown 
- Table at top, this is the table being queried
- extend AttackIP = extract(@"(\d{1,3}\.){3}\d{1,3}", 0, message)    Also used in attacker top IP query, creates a column for attacker IP and extracts the information from cowrie logs in the specific IP address format
- where isnotempty(AttackIP)                           makes sure to leave out logs that dont contain an IP address
- extend Geo = geo_info_from_ip_address(AttackIP)      Azure built in geo function, which can retrieve country, city, latitude and longitude, and others.
- extend Country = tostring(Geo.country)               takes out just the country input and puts it into a column
- summarize Attempts = count() by Country              collect the total count and groups it by country
- sort by Attempts desc                                sorts by the most common countries first
- Once complete, I can then change the time range and visualisation type, I decided to go for last 30 days and a world map
