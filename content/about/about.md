# Berkeley Housing Research
## Framework for Open Berkeley Data 
- Evolve a general data framework for municipalities to open all aspects of their permitting pipeline for access by data science analysts, general data science instruction, and the general public
- [Here's a first-pass at building a suite of JN to create the Annual Public Report for every city in California. ](https://colab.research.google.com/github/blockXblock/berkeley-housing-analysis/blob/main/notebooks/MASTER_ANALYSIS.ipynb#scrollTo=mR71p5MPDVqJ)
- Every city has a home-brew collection of databases, permit pipelines, spreadsheets, hacks and patches to satisfy the HCD annual report requirements
	- HCD has a least-common-denominator workflow for city reports, which degrades the data quality to an almost unusable level.
	- Berkeley uses Accela and Scala for open data access: terrible, does not allow bulk downloads of all permit or parcel data.  Can get 12,000 Berkeley business licenses, but totally inadequate to build city economic analysis of impact of new housing on city economy.
	- 

- See overview of today's City of Berkeley housing-related  data
	- Sadly outdated. Perhaps new Clariti contract can be re-negotiated
	- [[Berkeley Data Assets]]
### Illustrative Data Elements for Housing
- all relevant ordinances implementing California Housing Community Develeopment guidelines for annual municipal reporting
- timestamped components of permitting or inspecting any aspect of municipal housing
- Permit pipeline metadata 
    - allow analyis of progress of individual permit requests through the various stages of the pipeline
    - show references to the law cited as foundation of the permit request
      - AB2011
      - SB79
      - SB330
- Use Terner Center database of all California Legislation for updates
	- Sadly, it's incomplete, not kept up to date
	- Replace it with NotebookLM
	- Export to Datasette SQL open db