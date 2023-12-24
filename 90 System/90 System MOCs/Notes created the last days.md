---
up: "[[Home]]"
tags:
  - type/moc
---
```dataview
table "[[" + file.cday + "]]" as "Created" from !#type/highlights and !"90 System" WHERE (file.ctime >= date(today) - dur(5 day))
sort file.ctime
```
