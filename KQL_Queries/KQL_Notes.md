# Helpful KQL Info:

extend:  creates a new colum 
e.g extend AttackIP

where: Filters rows
e.g. where isnotempty(AttackIP)

summarise: groups and counts the field
e.g. summarise attempts = 

sort: sorts the chosen result
e.g. sort by attempts

take: limits the output by an amount
e.g. take 40

project: choose colums that you want to keep
e.g project TimeGenerated, message

bin: groups timestamps together
e.g. summarise attacks = count() by bin(generated)

extract: locate text inside a field
e.g. using extend AttackIP = extract(@"(\d{1,3}\.){3}\d{1,3}", 0, message) to pull IP info from logs

KQL uses '|' at each line as it passes the results step by step



