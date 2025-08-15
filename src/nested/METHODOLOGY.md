# Methodology

This document, other than following [the mdBook documentation](https://rust-lang.github.io/mdBook/), will detail the repository specific rules for creating new pages in this mdBook, the strategy for structuring chapters, and the lifecycle of information as it moves from a rough draft to a published chapter.

Specifically, the purpose of this page is to describe the design of the mdBook which catalogs the process of developing of the AI-assisted PKE system per our [Manifesto](/Manifesto.md).

We will use the P.A.R.A. method (Projects, Areas, Resources, Archive) as a conceptual guide to organize the top-level chapters and sections within this mdBook's **src** directory as the foundational information architecture for your mdBook project. In contrast to a freeform approach OR generally adaptible mdBook approach that fits appropriately to the software being documented and implemented simultaneously, this mdBook is somewhat self-referential in terms of developing a PKE, thus following the PARA structured, hierarchical approach from the outset makes sense for developing a PARA-influence PKE. 

In general, an issue-driven approach will be followed as we progress working through the daily modules in this mdBook's PKE development process, using the Zettelkasten concept of atomic notes. Each new issue that arises will be given it's own self-contained piece of research or issue#.md page.  At first the issue#.md page will be in the **1.Projects** folder until they are dispatched or dispositioned appropriately within the book's structure, all will be linked hierarchically by the SUMMARY.md file. 

The **1.Projects** folder will be the landing place for new issues and thereafter for short-term, less than one week efforts which are currently underway and should be regarded as *under HEAVY construction*. Issues that take on a larger life as much larger, ongoing effort will go to the **2.Areas** folder. Issues that are developed and completed will go to he **3.Resources** folder. Issues that are dismissed, after even a minor expenditure of dev effort, will go to the **4.Archive** folder.

The **2.Areas** folder will be for longer-term development and ongoing efforts that will stay open, perhaps indefinitely as *perhaps usable, but under ongoing development*. Areas that are developed for some time and eventually completed will go to he **3.Resources** folder.   

The **3.Resources** folder will be for usable references and material that's that have been either curated or developed and although curation might continue to add things, these items should be regarded as *stable enough to be considered usable, as good as complete*. In some cases, a Project or Area might graduate to being in its own development repository, but page linking to that effort will be maintained in the Resources folder. 

The **4.Archive** folder will be for things that *in the back Area 51 parking lot* and might still be valuable for informational purposes, but are basically not something anyone should use.  


 