---
up: "[[Ressources]]"
tags:
  - type/moc
created: 2024-01-05
---
```dataview
table category as "Category", date(born,"y-M-d G") as "Born", date(died,"y-M-d G") as "Dies" from #type/person and !"90 System"
```
