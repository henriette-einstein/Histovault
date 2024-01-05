History enthusiasts often have to deal with historical date values. As described in my previous blog post **Chronology Matters: Mastering Dates in Obsidian for a Better Grasp of History**, Obsidian has problems when dealing with B.C. date properties in the YAML front matter. I therefore recommended

1. Setting the property type of historical dates to “Text”
2. using historical dates with a “-” prefix if they are B.C.
3. using historical dates with a “+” prefix if they are A.D.

However, **there is a much better solution available!** 

The Dataview plugin uses the JavaScript library [Luxon](https://moment.github.io/luxon/#/) for parsing and formatting date and time values. This library can handle B.C. date values, however, the automated date parsing of Dataview does not. Therefore, the date(String, String) function provided by Dataview has to be used when dealing with date strings.

The following steps have to be done to support B.C. date properties in Obsidian when using the Dataview plugin:

1. Set the property type of historical dates to "Text"
2. Start writing all date properties using the format "y-M-d". To shorten the input, the year, month and day values are unpadded (for example `100-12-3` or `2024-1-1`)
3. Append the suffix "BC" if the date is a B.C. date (for example `100-7-12 BC`)
4. Append the suffix "AD" if the date is an A.D. date (for example `2024-1-1 AD`)

Using these steps, date properties are already quite readably when used in a Dataview list or table. 

## Problems

The suggested approach has some drawbacks:

1. Since Dataview treats date properties formatted using the steps described above as text values, the sort function produces 'wrong' results: A value of `2-1-1 BC` is interpreted as greater than a value `1-1-1 AD`, since the first character `2` is greater than the first character `1`.
2. It is not possible to extract the individual parts (year, month, day, era) of the date
3. It is not possible to perform calculations with the date values (e.g. calculate the duration between two dates)
## Solution

The problems can easily be solved by converting the date strings to date values. The Dataview plugin provides a utility function `date(text, format)` that can be used to perform the conversion.

A text property formatted as described above can be converted into a date property using the format string `y-M-d G`.
## Example

I use the same examples as in my previous post. We have two person notes, one for **Julius Caesar** (born 100-7-12 B.C., died 44-3-15 B.C.) and one for **Marcus Aurelius** (born 121-4-26 A.D., died 180-3-17 A.D.), whose dates of birth and death are set in the front matter of the notes.

In addition to that, I add another note for emperor **Augustus** (born 63-9-23 B.C., died 14-8-19 A.D.) to illustrate the sorting problems.

### Notes

In source-view, the notes now look as follows:

```
---  
tags: dictator  
born: 100-7-12 BC 
died: 44-3-15 BC 
---  
# Julius Caesar
```

```
---  
tags: emperor  
born: 121-4-26 AD 
died: 180-3-17 AD 
---  
# Marcus Aurelius
```

```
---
tags: emporer
born: 63-9-23 BC
died: 14-8-19 AD
---
# Augustus
```

### The Overview note

The following steps show how to implement an overview page, that displays the leaders of ancient Rome using the notes above and the Dataview plugin to generate a dynamic table 

An initial Dataview query 

```
table 
born as "Born", 
died as "Died" 
from #emperor or #dictator 
```

produces the following result
![[Initial Query.png]]
The result is unsorted. Therefore, the query should be enhanced by a sort command.

```
table 
born as "Born", 
died as "Died"
from #dictator or #emperor 
sort born
```

The result is "wrong": Augustus was born before Marcus Aurelius. That is because sorting a string produces different results than sorting a date value.
![[Sort.png]]
It is necessary to convert the "born" and "died" properties into dates using the date(text, format) function and also apply that conversion to the sort parameter to get correct results.

```
table 
date(born,"y-M-d G") as "Born", 
date(died,"y-M-d G") as "Died" 
from #emperor or #dictator 
sort date(born, "y-M-d G")
```

The results are slightly better readable and the sort command now produces correct results (Since I live in Germany, the output uses the German names for the months. The output in other countries may vary).

![[Sort by Date.png]]
The output can be enhanced further, by tweaking the Date Format setting to `DDDD GG` in the Dataview plugin settings. 

![[Dataview settings.png]]

The resulting output then looks as follows (in German "v. Chr." means B.C. and "n. Chr." means A.D.);
![[Change Display settings.png]]
With the date properties converted to date values, it is now also possible to extract the date parts easily. For example, it is possible to display only the years of birth and death. 

```
table 
date(born,"y-M-d G").year as "Born", 
date(died,"y-M-d G").year as "Died" 
from #emperor or #dictator 
sort date(born, "y-M-d G")
```

That results in the following output:
![[Year of Birth and Death.png]]
Even calculations are possible, like displaying the age of the person:
```
table 
date(born,"y-M-d G") as "Born", 
date(died,"y-M-d G") as "Died",
durationformat(date(died,"y-M-d G") - date(born,"y-M-d G"),"y 'years' M 'month'")  as "Age"
from #dictator or #emperor 
sort date(born, "y-M-d G")
```

![[Calculate Age.png]]
## Summary
The solution presented here may result in a little lengthier Dataview queries, but overall, the results are worth it.

It would be beneficial if the Dataview plugin had a customizable setting for the format used to parse text values into dates. Even better, if the date mechanism in Obsidians front matter implementation would support B.C. dates. 

However, I think the provided solution may help in using B.C. dates in Obsidian until then.
# See also
- [How to organize sortable date fields which can include CE and BCE dates? - Help - Obsidian Forum](https://forum.obsidian.md/t/how-to-organize-sortable-date-fields-which-can-include-ce-and-bce-dates/66494/8)