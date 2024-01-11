---
up: "[[Ressources]]"
tags:
  - type/moc
created: 2024-01-05
---
```dataview
table category as "Category", date(born,"y-M-d G") as "Born", choice(!died,"--",date(default(died,"2030-01-01 AD"),"y-M-d G")) as "Died" from #type/person and !"90 System"
```
