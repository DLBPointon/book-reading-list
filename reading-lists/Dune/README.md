# Dune - Universal Reading List

Contains 6 series organised as Chronological to the events they contain.

Any Supplementary material to be added to each series should follow the following:

Original Series File:
```
	<Series Name="Dune">
		<Database Name="Hardcover" Item="dune" />
	</Series>
```

Supplementary Series File:
```
	<Series Name="Dune" Subtype="Supplementary" Position="-1">
		<Database Name="Hardcover" Item="dune" />
	</Series>
```

The idea is that this would "bind" it to the Dune Series.
