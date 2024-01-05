---
up: "[[People]]"
tags:
  - type/moc
created: 2024-01-05
---

```dataview
table date(born,"y-M-d G") as "Born", date(died,"y-M-d G") as "Died" from #type/person 
where category = [[]]
```
