
## Purpose
- Display Information about notes that deal with information about a historical period
	- Events
	- People (Born, died)
- Period can be defined as needed (A century, a decade, a year, a month).

History enthusiasts often want to get a quick overview of notes attached to historical dates. One example is an overview of the dates of birth and death of historical figures. Another example is an overview of historical events that occurred in a defined period in time, for example, the 20th Century.

Obsidian and the Dataview plugin make it easy to create notes that provide an overview of notes that fall in a historical period. This article describes what you have to do, to create such overview notes, and provides a bunch of Obsidian templates that can be used as an entry point for such an effort.


## Tags and Metadata
To produce the desired results, notes about events and people have to be tagged and must contain specific metadata that can be used by the Dataview plugin. 

All notes that are about people are tagged with the tag *type/person*.

All notes that are about events are tagged with the tag *type/event*.

## Categories
Both people and events can fall into special categories. People may, for example, belong to the category "Soldier", "Politician" or "Artist". Events may be categorized as "Conflict", "Conference" or "Earthquake". What categories are useful depends on your studies and the purpose of your Knowledge Base.

There are basically two ways to encode categories in your notes:

1. You can associate sub-tags like **person/politician** to a note, or
2. You can use a specific metadata property like **category** and attach that to a note

I prefer the second approach, since I want to display the Category in the result of the Dataview queries.