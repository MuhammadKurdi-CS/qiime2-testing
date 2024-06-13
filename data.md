What is QIIME 2?

QIIME 2 is a powerful, extensible, and decentralized microbiome analysis package with a focus on data and analysis transparency. QIIME 2 enables researchers to start an analysis with raw DNA sequence data and finish with publication-quality figures and statistical results.

Key features:

- Integrated and automatic tracking of data provenance

- Semantic type system

- Plugin system for extending microbiome analysis functionality

- Support for multiple types of user interfaces (e.g. API, command line, graphical)

QIIME 2 is a complete redesign and rewrite of the QIIME 1 microbiome analysis pipeline. QIIME 2 will address many of the limitations of QIIME 1, while retaining the features that makes QIIME 1 a powerful and widely-used analysis pipeline.

QIIME 2 currently supports an initial end-to-end microbiome analysis pipeline. New functionality will regularly become available through QIIME 2 plugins. You can view a list of plugins that are currently available on the QIIME 2 plugin availability page. The future plugins page lists plugins that are being developed.

This page describes several core concepts in QIIME 2 that are important to understand before starting to use the software. The glossary may be helpful to refer to as you read through this page and other documentation on the site.

Data files: QIIME 2 artifacts
Data produced by QIIME 2 exist as QIIME 2 artifacts. A QIIME 2 artifact contains data and metadata. The metadata describes things about the data, such as its type, format, and how it was generated (provenance). A QIIME 2 artifact typically has the .qza file extension when stored in a file.

Since QIIME 2 works with artifacts instead of data files (e.g. FASTA files), you must create a QIIME 2 artifact by importing data. You can import data at any step in an analysis, though typically you will start by importing raw sequence data. QIIME 2 also has tools to export data from an artifact. See the importing guide for details.

By using QIIME 2 artifacts instead of simple data files, QIIME 2 can automatically track the type, format, and provenance of data for researchers. Using artifacts instead of data files enables researchers to focus on the analyses they want to perform, instead of the particular format the data needs to be in for an analysis.

Artifacts enable QIIME 2 to track, in addition to the data itself, the provenance of how the data came to be. With an artifact’s provenance, you can trace back to all previous analyses that were run to produce the artifact, including the input data used at each step. This automatic, integrated, and decentralized provenance tracking of data enables a researcher to archive artifacts, or for example, send an artifact to a collaborator, with the ability to understand exactly how the artifact was created. This enables replicability and reproducibility of analyses, as well as generation of diagrams and text that can be used in the methods section of a paper. Provenance also supports and encourages the proper attribution to underlying tools (e.g. FastTree to build a phylogenetic tree) used to generate the artifact.

Note

It has been brought to our attention that the term artifact may be confusing, as it is frequently used by biologists to refer to a source of experimental bias. We use the term artifact here to mean an object that is made by some process (similar, for example, to an archaeological artifact). Throughout our documentation and other educational materials, we try to clarify that we are talking about QIIME 2 artifacts as they are defined in this section.

Data files: visualizations
Visualizations are another type of data generated by QIIME 2. When written to disk, visualization files typically have the .qzv file extension. Visualizations contain similar types of metadata as QIIME 2 artifacts, including provenance information. Similar to QIIME 2 artifacts, visualizations are standalone information that can be archived or shared with collaborators.

In contrast to QIIME 2 artifacts, visualizations are terminal outputs of an analysis, and can represent, for example, a statistical results table, an interactive visualization, static images, or really any combination of visual data representations. Since visualizations are terminal outputs, they cannot be used as input to other analyses in QIIME 2.

Tip

Use https://view.qiime2.org to easily view QIIME 2 artifacts and visualizations files (generally .qza and .qzv files) without requiring a QIIME installation. This is helpful for sharing QIIME 2 data with collaborators who may not have QIIME 2 installed. https://view.qiime2.org also supports viewing data provenance.

Semantic types
Every artifact generated by QIIME 2 has a semantic type associated with it. Semantic types enable QIIME 2 to identify artifacts that are suitable inputs to an analysis. For example, if an analysis expects a distance matrix as input, QIIME 2 can determine which artifacts have a distance matrix semantic type and prevent incompatible artifacts from being used in the analysis (e.g. an artifact representing a phylogenetic tree).

Semantic types also help users avoid semantically incorrect analyses. For example, a feature table could contain presence/absence data (i.e., a 1 to indicate that an OTU was observed at least one time in a given sample, and a 0 to indicate than an OTU was not observed at least one time in a given sample). However, if that feature table were provided to an analysis computing a quantitative diversity metric where OTU abundances are included in the calculation (e.g., weighted UniFrac), the analysis would complete successfully, but the result would not be meaningful.

Check out the semantic types page for more information about semantic types and what types are currently available.

Plugins
QIIME 2 microbiome analyses are made available to users via plugins. To perform analyses with QIIME 2, you will install one or more plugins that provide the specific analyses you are interested in. For example, if you want to demultiplex your raw sequence data, you might use the q2-demux QIIME 2 plugin, or if you’re wanting to perform alpha- or beta-diversity analyses, you could use the q2-diversity plugin.

Plugins are software packages that can be developed by anyone. The QIIME 2 team has developed several plugins for an initial end-to-end microbiome analysis pipeline, but third-party developers are encouraged to create their own plugins to provide additional analyses. Third-party developers will define these plugins in the same way that the QIIME 2 team has defined the “official” plugins. This decentralized development of microbiome analysis functionality means that many more analyses and tools will be accessible to QIIME 2 users, including the latest techniques and protocols. Plugins also allow users to choose and customize analysis pipelines for their specific needs.

Check out the plugin availability page to see what plugins are currently available and the future plugins page for those that are being developed.

Methods and visualizers
QIIME 2 plugins define methods and visualizers that are used to perform analyses.

A method accepts some combination of QIIME 2 artifacts and parameters as input, and produces one or more QIIME 2 artifacts as output. These output artifacts could subsequently be used as input to other QIIME 2 methods or visualizers. Methods can produce intermediate or terminal outputs in a QIIME 2 analysis. For example, the rarefy method defined in the q2-feature-table plugin accepts a feature table artifact and sampling depth as input and produces a rarefied feature table artifact as output. This rarefied feature table artifact could then be used in another analysis, such as alpha diversity calculations provided by the alpha method in q2-diversity.

A visualizer is similar to a method in that it accepts some combination of QIIME 2 artifacts and parameters as input. In contrast to a method, a visualizer produces exactly one visualization as output. Visualizations, by definition, cannot be used as input to other QIIME 2 methods or visualizers. Thus, visualizers can only produce terminal output in a QIIME 2 analysis.
