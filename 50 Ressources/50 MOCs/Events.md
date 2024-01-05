---
up: "[[Ressources]]"
tags:
  - type/moc
created: 2024-01-05
---
```dataview
table category as "Category", date(start,"y-M-d G") as "Start", date(end,"y-M-d G") as "End" from #type/event and !"90 System"
sort date(start,"y-M-d G")
```
