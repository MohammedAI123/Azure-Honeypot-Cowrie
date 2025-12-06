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


