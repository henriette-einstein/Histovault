## Initial Query

```dataview
table 
died as "Born", 
born as "Died"
from #dictator or #emperor 
```

## Sort

```dataview
table 
born as "Born", 
died as "Died"
from #dictator or #emperor 
sort born
```

## Convert to dates

```dataview
table 
dateformat(date(born,"y-M-d G"),"MMMM d, y") as "Born", 
dateformat(date(died,"y-M-d G"), "MMMM d, y") as "Died" 
from #emperor or #dictator 
sort born
```

## Sort by date

```dataview
table 
dateformat(date(born,"y-M-d G"),"MMMM d, y") as "Born", 
dateformat(date(died,"y-M-d G"), "MMMM d, y") as "Died" 
from #emperor or #dictator 
sort date(born, "y-M-d G")
```

## Change display settings

```dataview
table 
date(born,"y-M-d G") as "Born", 
date(died,"y-M-d G") as "Died" 
from #emperor or #dictator 
sort date(born, "y-M-d G")
```


## Year of Birth and Death

```dataview
table 
date(born,"y-M-d G").year as "Born", 
date(died,"y-M-d G").year as "Died" 
from #emperor or #dictator 
sort date(born, "y-M-d G")
```

## Calculate Age

```dataview
table 
date(born,"y-M-d G") as "Born", 
date(died,"y-M-d G") as "Died",
durationformat(date(died,"y-M-d G") - date(born,"y-M-d G"),"y 'years' M 'month'")  as "Age"
from #dictator or #emperor 
sort date(born, "y-M-d G")
```