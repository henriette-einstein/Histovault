---
up: "[[Events]]"
tags:
  - type/moc
---
```dataview
table eventcategory as "category", start, end from #type/event  and !"90 System" where eventcategory = [[]]
```