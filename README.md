# Book Reading List format

Currently, every platform has an internal list which catalouges reading lists. Comic books, on the other hand have CBL (Comic Book List) which details the comic series, volumes and issues which need to be bound together for a particular Story Line.

As far as i'm aware, nothing similar exists for books. For very large book series, which encompass a universe of works, the concept of a series can be nested.

The aim of brl is to create an open format for easily sharing book lists which can be adopted by popular book reading programs/tool/sites.

- [Warhammer 40K](./Warhammer_40k/README.md)

    - As a simple example contains The Inquisitor Series, which in turn contains the Eisenhorn Series, Ravenor Series and Bequin Series.

- [Dune](./Dune/README.md)

    - Containing 6 distinct series which I've written up in brl as an example case. This currently does not contain any nested series such as supplementary material.

- Discworld

- Cosmere

I'm sure there are many many more.

This is all further complicated by `Supplementary books`, which have no place in the main series but offer further insight into the series or may simply explain the vehicles and lore of the universe (Codex's form Warhammer, Bestiaries from various universes and so on). In my opion Supplementary material should be a series nested inside it's parent series, for example `Series` would contain `Subtype` (the nested series) of `Supplementary`. In the case of `<Series Name="Dune" Subtype="Supplementary Works">` and be resolved as `Dune: Supplementary Works`. How this works will need further discussion with the community.

## Solution

This isn't a perfect solution, however, I propose a format based on CBL specific for book. We can call this BRL (Book reading lists).

The aim is to be a open source format, with a central and documented format to allow for easy replication of reading lists. This could be an official series list, a personal reading list or another `50 Best Sci-Fi of the last century` lists. The aim is for easy sharing.

### CBL

I learnt about the CBL format from the [Kavita](https://github.com/Kareadita/Kavita) Discord, specifically from a repo one of their very prominant members formed for sharing comic book reading lists. [DieselTech's](https://github.com/DieselTech/CBL-ReadingLists) comunity repo is a plethora of reading lists covering everything in comics books from what must be the Cocaine fueled minds of Zenoscope to the world changing Age of Krakoa Era comics from Marvel.

The format is something like this:

```
<?xml version="1.0" encoding="utf-8"?>
<ReadingList xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
<Name>[X-Men Krakoa 0.1] House of X Powers of X</Name>
<NumIssues>12</NumIssues>
<Books>
<Book Series="House of X" Number="1" Volume="2019" Year="2019">
<Database Name="cv" Series="120309" Issue="714236" />
</Book>
<Book Series="Powers of X" Number="1" Volume="2019" Year="2019">
<Database Name="cv" Series="120407" Issue="714669" />
</Book>
<Book Series="House of X" Number="2" Volume="2019" Year="2019">
<Database Name="cv" Series="120309" Issue="715306" />
</Book>
...9 other Books
</Books>
<Matchers />
</ReadingList>
```

Now I tried to use this format for books for it falls short unless all books are effectively in a series of 1 and you stich them together through this reading list. It simply doesn't work well.

My proposal is a format something more on the line of:

```
<?xml version="1.0" encoding="UTF-8"?>
<ReadingList>
	<Universe Name="Dune"/>
	<Series Name="The Caladan Trilogy" Position="5">
		<Database Name="Hardcover" Item="the-caladan-trilogy" />
	</Series>
	<NumBooks>3</NumBooks>
	<Books>
		<Book Name="Dune: The Duke of Caladan" Year="1978">
			<Database Name="Hardcover" Item="dune-the-duke-of-caladan" />
		</Book>
		<Book Name="Dune: The Lady of Caladan" Year="2021">
			<Database Name="Hardcover" Item="dune-the-lady-of-caladan" />
		</Book>
		<Book Name="Dune: The Heir of Caladan" Year="2022">
		    <Database Name="Hardcover" Item="dune-the-heir-of-caladan" />
		</Book>
	</Books>
</ReadingList>
```

### Tags

#### ReadingList
Top level tag containing all other Tags.

#### Universe
The universe tag is intended to act as the parent tag word of multiple series.

This could then be used to create pages to collect works in a `Universe` into some kind of order.

- `Name`: name of the Universe
- `Position`: Position of series in the Universe

#### Series
This would be the essential naming of a collection of book.

It can consist of:
- `Name`: name of the series
- `Subtype` (happy to change this to something more suiting): name of subseries
- `Position`: position of series in Universe, this is needed more when there is a `Subtype`
- `Database`: Collection of information that could be used to confirm series positioning.

This way we can have:
`<Series Name="The Horus Heresy" Subtype="Main" Position="1">`

To place the series as the first series of the Horus Heresy in the Warhammer 40k Universe with the name `The Horus Heresy: Main`. This then makes further additions simpler and automatically grouped, each line would be in a new file.

`<Series Name="The Horus Heresy" Subtype="Primarchs" Position="2">`

`<Series Name="The Horus Heresy" Subtype="Characters" Position="3">`

`<Series Name="The Horus Heresy" Subtype="Suplementary" Position="-1">`

#### Database
As above, `Database` collects information used to confirm a book or series list.
- `Name`: One of ["Hardcover", "Goodreads", "Google", "Amazon"]
- `item`: Unique ID of that item on that site. For example, the book `False Gods` of the Horus heresy has the unique code of `false-gods`. It isn't always as simple as this however, `Goodreads` code for the same book is `381817.False_Gods`

#### Books
Collection of Book.

#### Book
Individual Book data consisting of:
- `Name`: Name of the book.
- `Year`: Year of publication to narrow down matches.
- `Publisher`: Publisher of book - Optional

Book can also encompass a `Database` in the same way as `Series`.
