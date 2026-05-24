# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A 10-minute talk at [FORCE 2026](https://www.force11.org/) (3–5 June 2026, Singapore) titled **"How KAUST Library Uses DataCite"**. The presenter (Marcelo Garcia) was invited because he will attend FORCE anyway; he was not the architect of the systems described. The framing is explicitly "standing on the shoulders of a giant" — referring to Daryl Grenz, the previous KAUST IR lead who built the DataCite + ORCID + DSpace integrations. Tone is positive and honest about what was built by others.

## Source material

`~/Documents/DataCite_FORCE_2026/DOI_Workflow_Best_Practices-Adding_Person_Affiliation_Relationship_Connections_DataCite_Metadata_Records.pdf` — 20-slide KAUST Library presentation by Daryl Grenz and Rawan Karsou, given at the DataCite Annual Committee Meeting, October 2023. This is the primary content source.

## Narrative structure (9 slides)

1. **Title** — "How KAUST Library Uses DataCite", Marcelo Garcia, FORCE 2026
2. **Standing on the shoulders of a giant** — explicitly credit Daryl Grenz; Newton's quote used to frame the talk, not as a label for Daryl; timeline: DSpace IR (2011), ORCID integration (2015), DataCite membership (2018)
3. **What we register DOIs for** — theses and dissertations are the core (KAUST's unique collection); treemap showing dominance of theses + dissertations, with growing diversity of other types (datasets, software, posters, etc.)
4. **Making people visible — ORCID** — required for theses/dissertations since 2015; proactively added for confirmed KAUST authors on datasets; 86% theses/dissertations and 82% datasets have ORCID iDs
5. **Making institutions visible — ROR** — text affiliation (2018) → KAUST ROR ID added (2022); scope limited to KAUST-only authors due to DSpace form constraints
6. **Making relationships visible — dataset↔article links** — `IsSupplementTo` / `IsSupplementedBy`; library manually follows up to add DOIs for related articles once published
7. **The unfinished project — reference lists in ETDs** — the insight (thesis citations are invisible to the scholarly graph); the pilot (BibTeX → DataCite `relatedItems` with `References` relationType); what worked (infrastructure ready, DataCite Commons shows it well); what didn't (only 7/200 authors submitted BibTeX)
8. **A direction worth exploring** — a separate semantic search project already converts KAUST thesis PDFs to Markdown using [docling](https://www.docling.ai/); this text layer *could* enable automatic reference extraction without asking authors; framed cautiously as a potential path, not a roadmap
9. **Questions / Thank you** — credit Daryl Grenz and Rawan Karsou

## The full timeline of Daryl's work

This was built incrementally by Daryl Grenz (and collaborators Rawan Karsou, Yasmeen Alsaedy, Mohyden Habbal, Mohamed Ba-Essa):

- **2009** — KAUST founded
- **2011** — DSpace institutional repository established (started in SharePoint, moved to DSpace)
- **2012** — Handle identifiers added for ETDs (persistent links, predating DOIs)
- **2014** — Early adopter of ORCID; required ORCID iD for all thesis/dissertation submissions; ORCID integration also pushes ETD metadata *to* the student's ORCID record; faculty advisors and committee members searchable by ORCID iD
- **2018** — DataCite membership; DOIs registered via a **custom DOI Minter** (see OR2019 poster)
- **2019** — OR2019 poster presenting the DOI Minter architecture (Habbal & Grenz)
- **2021** — ETD2021 presentation on using PIDs to enhance thesis services; mentions Wikidata and Semantic Scholar as future aspirations
- **2022** — KAUST ROR ID added to affiliation entries
- **2023** — DataCite Annual Committee Meeting presentation on person/affiliation/relationship connections

## The DOI Minter — architectural key detail

The OR2019 poster describes why metadata enrichment was possible: Daryl built a **custom DOI Minter service** connected to DSpace via REST API, *separate from DSpace itself*. Native DSpace DataCite integration was too limited (no enrichment of ORCID iDs, affiliations, relationships), and KAUST uses commercial hosting which makes in-platform customisation risky for upgrades. The separate service provides on-demand triggering, full metadata enrichment, and room for future extension. This is why KAUST can do things with DataCite metadata that most DSpace institutions cannot.

## Key facts from the 2023 source presentation

- Repository platform: DSpace (v7 as of recent upgrade)
- DOI prefix: 10.25781
- Item types with DOIs: Thesis, Dissertation, Dataset, Poster, Protocol, Software, Video, Presentation, Student Guide, Technical Report, Web Page
- ORCID coverage: 86% theses/dissertations, 82% datasets
- Affiliation: text-only (2018), ROR ID added (2022); KAUST-only authors
- Relationship pilot numbers (2023): Software with IsSupplementTo=2, Datasets with IsSupplementTo=19, Thesis/Dissertation with IsSupplementedBy=5, Thesis/Dissertation with References=6
- Reference list pilot: 200 authors emailed → 16 responses → 7 records enriched; BibTeX converted to XML via PHP; automatic notification set up for new graduates
- DataCite mapping decision: `relatedItems` for all references + `relatedIdentifier` when DOI/URL exists; `References` relationType (treated as equivalent to `Cites`)
- Caveat: removing a `relatedIdentifier` does NOT remove the citation from DataCite Commons

## Additional source documents

- `~/Documents/DataCite_FORCE_2026/ETD2021_Presentation_Proposal.pdf` — ETD2021 proposal by Grenz et al., "Using Persistent Identifiers to Enhance Thesis and Dissertation Services"; good narrative overview of the ORCID and DataCite work; mentions Wikidata and Semantic Scholar as future aspirations
- `~/Documents/DataCite_FORCE_2026/OR2019 poster proposal DOIMinter.pdf` — OR2019 poster by Habbal & Grenz explaining the custom DOI Minter architecture and the rationale for keeping it separate from DSpace

## Presenter context

Marcelo Garcia was not directly involved in building the repository integrations. He was invited to present because he will be at FORCE 2026. He is separately working on a **semantic search project** that converts KAUST thesis/dissertation PDFs to Markdown using docling — a pipeline already in place that could, in the future, be used to extract reference lists automatically and resume the unfinished ETD reference pilot.

## Repository Structure

- `slides/DataCiteForce2026.tex` — Beamer presentation source (skeleton to be filled in Overleaf)

## Workflow

The presentation is authored and compiled in **Overleaf**. This repository is for discussing and planning slide *content* — what to say, what to include, how to structure the narrative — not for building or editing LaTeX directly.

The `.tex` file here serves as a reference snapshot of the current slide content.

## Beamer Notes

The presentation uses the default Beamer theme with `aspectratio=169` (16:9). Each slide is a `\begin{frame}...\end{frame}` block.
