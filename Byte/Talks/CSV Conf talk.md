No single-file data dump that's platform agnostic? Many problems!

I couldn't find a standard to export a hierarchical relational database into a single file (or file system) that preserved relationships and hierarchies but also didn't force IDs or other ephemeral data, so I did the worst thing possible: I created my own standard. Here's how one bad decision led to a series of bad decisions, but also led to a single-file, platform-agnostic, relationship- and hierarchy-preserving data dump. (Let's find a better system?)

---

Let's say we have a relational database, mysql or sqlite or postgres or whatever, and want to export the data so it can be imported into a different database or database type. We don't, however, want to keep the exact IDs for the records, because we're merging the data into a greater data set, and the IDs are taken already, or we're merging into an independent data set, and we don't want our first record to have an ID of 512593, because we're on the OCD spectrum.

We can export a series of CSV or JSON files, and we'll have set IDs, and we can programmatically run through each record, create an old to new IDs temporary table, and ensure our relationships are maintained through python or php or whatever. Or we could create slugs for relationships, but that will assuredly fall apart when merging several data sets.


Modern data, in what is considered as "good librarianship", is saving data in Github repos with front matter holding the data. Of course means that no data connections are enforced, and hierarchies could fall apart by deleting a parent, not to mention typos and other human error breaking everything.

What would be a gold standard?

* It should be able to be one file, like a SQL dump
* It should be human readable
* A full entity-relationship diagram could be generated from the file
* A basic entity-relationship diagram could be at the top of the file

