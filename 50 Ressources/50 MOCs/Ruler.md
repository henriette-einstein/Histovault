---
up: "[[People]]"
tags:
  - type/moc
created: 2024-01-05
---

```dataview
table 
date(born,"y-M-d G") as "Born", 
choice(!died,"--",date(default(died,"2030-12-31"),"y-M-d G")) as "Died" from #type/person 
where category = [[]]
```
