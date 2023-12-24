---
up: "[[Home]]"
tags:
  - type/moc
---
```dataview
table "[[" + file.cday + "]]" as "Created" from "40 Sources/40 Highlights" WHERE (file.ctime >= date(today) - dur(5 day))
sort file.ctime
```
