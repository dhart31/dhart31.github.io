# Research Study Archetypes

This directory contains Hugo archetypes (templates) for creating blog posts about different types of research studies. Each archetype follows the appropriate EQUATOR reporting guideline to ensure comprehensive and standardized documentation.

## Available Archetypes

### Observational Studies (STROBE Guidelines)

1. **cohort-study.md** - For prospective or retrospective cohort studies
2. **case-control.md** - For case-control studies
3. **cross-sectional.md** - For cross-sectional studies

### Qualitative Research

4. **qualitative.md** - For qualitative research (COREQ guidelines)
   - Interviews
   - Focus groups
   - Other qualitative methods

### Experimental Studies

5. **rct.md** - For randomized controlled trials (CONSORT 2025 guidelines)

### Evidence Synthesis

6. **systematic-review.md** - For systematic reviews and meta-analyses (PRISMA 2020 guidelines)

## How to Use

### Create a new blog post using an archetype:

```bash
# For a cohort study
hugo new posts/my-cohort-study/index.md --kind cohort-study

# For a case-control study
hugo new posts/my-case-control-study/index.md --kind case-control

# For a cross-sectional study
hugo new posts/my-cross-sectional-study/index.md --kind cross-sectional

# For qualitative research
hugo new posts/my-qualitative-study/index.md --kind qualitative

# For a randomized controlled trial
hugo new posts/my-rct/index.md --kind rct

# For a systematic review
hugo new posts/my-systematic-review/index.md --kind systematic-review
```

### Alternatively, use the default archetype:

```bash
hugo new posts/my-post/index.md
```

## Reporting Guidelines Reference

Each archetype is based on internationally recognized reporting guidelines:

- **STROBE** (Strengthening the Reporting of Observational Studies in Epidemiology)
  - [STROBE Statement](https://www.strobe-statement.org/)
  - [EQUATOR Network - STROBE](https://www.equator-network.org/reporting-guidelines/strobe/)

- **COREQ** (Consolidated Criteria for Reporting Qualitative Research)
  - [EQUATOR Network - COREQ](https://www.equator-network.org/reporting-guidelines/coreq/)

- **CONSORT** (Consolidated Standards of Reporting Trials)
  - [CONSORT Statement](http://www.consort-statement.org/)
  - [EQUATOR Network - CONSORT](https://www.equator-network.org/reporting-guidelines/consort/)

- **PRISMA** (Preferred Reporting Items for Systematic Reviews and Meta-Analyses)
  - [PRISMA Statement](http://www.prisma-statement.org/)
  - [EQUATOR Network - PRISMA](https://www.equator-network.org/reporting-guidelines/prisma/)

## Customizing Templates

Each archetype contains placeholder text in brackets `[like this]`. When writing your blog post:

1. Replace all bracketed text with your actual content
2. Delete sections that are not applicable to your study (marked with "if applicable")
3. Keep the overall structure to ensure comprehensive reporting
4. Update the tags in the front matter as needed

## Front Matter

All archetypes use YAML front matter with the following fields:

```yaml
---
title: "Post Title"
date: 2025-02-13
showToc: true
summary: "Brief summary"
tags: ["study-type", "relevant-tags"]
draft: true
---
```

Remember to set `draft: false` when you're ready to publish!

## Additional Resources

- [EQUATOR Network](https://www.equator-network.org/) - Comprehensive database of reporting guidelines
- [EQUATOR Network Wizard](https://www.goodreports.org/) - Tool to help select appropriate reporting guideline
- Full checklists are available in the `/checklists` directory

## Notes

- The templates are comprehensive and include all checklist items from the respective guidelines
- Not all items may be relevant to every study - use your judgment
- Consider these templates as starting points; adapt them to your specific needs
- When in doubt, refer to the original reporting guideline documentation
