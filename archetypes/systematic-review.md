---
title: "{{ replace .File.ContentBaseName "-" " " | title }}"
date: {{ .Date }}
showToc: true
summary: ""
tags: ["systematic-review", "meta-analysis", "prisma"]
draft: true
---

**Study Design:** Systematic Review [and Meta-Analysis]

## Title and Abstract

**Title:**
[Identify the report as a systematic review in the title]

**Structured Abstract:**
[Report an abstract addressing each item in the PRISMA 2020 for Abstracts checklist]

## Introduction

### Rationale
- Describe the current state of knowledge and its uncertainties
- Articulate why it is important to do the review
- If other systematic reviews exist, explain why current review was necessary
- If examining effects of interventions, describe how intervention(s) might work

### Objectives
- Provide explicit statement of objective(s) or question(s) using PICO framework or variant:
  - **Population:**
  - **Intervention:**
  - **Comparator:**
  - **Outcome:**

## Methods

### Eligibility Criteria
- Specify study characteristics used to decide eligibility (PICO and other characteristics):
  - Study design(s):
  - Setting(s):
  - Minimum duration of follow-up:
- Eligibility criteria for report characteristics: [year, language, report status]
- Clearly indicate if studies were ineligible because outcomes not measured or results not reported
- Specify groups used in synthesis and link to comparisons in objectives
- Rationale for notable restrictions to study eligibility

### Information Sources
- Specify date when each source was last searched or consulted
- For bibliographic databases: name, interface/platform, coverage dates
- For study registers: name, date restrictions
- For websites/search engines: name and URL
- For organisations/manufacturers contacted: name
- For individuals contacted: types, authors of included studies
- For reference lists: types of references
- For citation searches: bibliographic details
- For crowdsourcing: platform and dates
- For other sources: name

### Search Strategy
- Full line-by-line search strategy for at least one database
- Limits applied and justification
- Published approaches used (if any) with changes made
- Natural language processing/text frequency tools (if used)
- Tool for automating translation (if used)
- Validation of search strategy (if done)
- Peer review process (if done)
- Final conceptual structure (if not PICO-based)

### Selection Process
- Number of reviewers screening each record and each report
- Whether multiple reviewers worked independently
- Processes to resolve disagreements
- Processes to obtain or confirm relevant information
- Translation requirements and how handled
- Automation tools in selection process (if used)
- Crowdsourcing (if used)
- Datasets of already-screened records (if used)

### Data Collection Process
- Number of reviewers collecting data from each report
- Whether multiple reviewers worked independently
- Processes to resolve disagreements
- Processes to obtain or confirm data
- Automation tools for data collection (if used)
- Software used to extract data
- Decision rules for selecting data from multiple reports

### Data Items (Outcomes)
- List and define outcome domains and timeframe
- Whether all compatible results sought
- Changes to inclusion/definition of outcome domains with rationale
- Changes to select results within eligible domains with rationale
- Which outcome domains most important for conclusions and rationale

### Data Items (Other Variables)
- List and define all other variables sought
- Assumptions about missing/unclear information
- Tool used to collect data items (if used)

### Study Risk of Bias Assessment
- Tool(s) and version used
- Methodological domains/components/items of tool used
- Overall risk of bias judgement and rules
- Adaptations to existing tool (if made)
- New tool developed (if applicable, describe and make publicly accessible)
- Number of reviewers assessing risk of bias per study
- Whether multiple reviewers worked independently
- Processes to resolve disagreements
- Processes to obtain or confirm information
- Automation tool used (if applicable)

### Effect Measures
- For each outcome: effect measure(s) used in synthesis or presentation
- Thresholds/ranges for interpreting effect size
- Method to re-express results to different effect measure (if used)
- Justification for choice of effect measure

### Synthesis Methods

**Eligibility for Synthesis:**
[Processes to decide which studies were eligible for each synthesis]

**Preparing for Synthesis:**
[Methods to prepare data for synthesis]

**Tabular and Graphical Methods:**
[Tabular structure(s) and graphical method(s) used]
[If studies ordered/grouped, basis for ordering/grouping]

**Statistical Synthesis:**
[Statistical method(s) used]
[If no statistical synthesis possible, explain why]
[Software/packages and version numbers]

**If Meta-Analysis:**
- Meta-analysis model: [fixed-effect, fixed-effects, or random-effects]
- Rationale for model
- Between-study variance estimator (for random-effects)
- Method to calculate confidence intervals (for random-effects)
- Any methods to identify/quantify statistical heterogeneity
- If random-effects: prior distributions, computational choices, effect measure with credible intervals

**If Multiple Effect Estimates per Study:**
[Method(s) to model or account for statistical dependency]

**If Multilevel Models/Robust Variance Estimation:**
[Method(s) used]

**If Synthesis Not Considered or Appropriate:**
[Reason and decision process]

### Reporting Bias Assessment
- Methods to assess risk of bias due to missing results
- Tool used (if applicable)
- Adaptations to existing tool (if made)
- New tool developed (if applicable)
- Number of reviewers assessing risk
- Processes to resolve disagreements
- Processes to obtain or confirm information
- Automation tool (if used)

### Certainty Assessment
- Tool/system and version used
- Factors considered
- Decision rules for overall judgement
- Intended interpretation of each certainty level
- Thresholds for imprecision and ranges
- Adaptations (if made)
- Number of reviewers assessing certainty
- Processes to resolve disagreements
- Processes to obtain or confirm information
- Automation tool (if used)

## Results

### Study Selection

**Flow Diagram:**
- Records identified:
- Records excluded before screening:
- Records screened:
- Records excluded:
- Reports retrieved for detailed evaluation:
- Potentially eligible reports not retrievable:
- Retrieved reports assessed for eligibility:
- Reports excluded with reasons:
- Studies included in review:
- Reports of included studies:

[If update: number of studies in previous review, search and selection process, number included in current review]

[If automation tools used: number excluded by human vs automation]

**Excluded Studies:**
[Cite studies that might appear to meet inclusion criteria but were excluded, with reasons]

### Study Characteristics
[Cite each included study]
[Present key characteristics in table or figure]
[If examining intervention effects: consider table summarising intervention details for each study]

### Risk of Bias in Studies
[Present tables/figures indicating risk of bias in each domain/component/item for each study and overall study-level risk]
[Present justification for each judgement via quotations from included studies]
[If risk of bias assessments for specific outcomes or results: consider displaying on forest plot or tables]

### Results of Individual Studies
[For all outcomes (whether statistical synthesis undertaken): present summary statistics with confidence intervals for each group and effect estimate with precision]
[For dichotomous outcomes: report number with event and total in each group]
[For continuous outcomes: report mean, SD, and sample size]
[If study-level data presented visually/reported in text: also present tabular display]
[If applicable: indicate which results not directly reported and had to be computed]

### Results of Syntheses

**Characteristics of Syntheses:**
[Brief summary and risk of bias among studies for each synthesis]
[Indicate studies contributing]

**Results:**
[Present results of all syntheses in protocol and not prespecified]

**For Meta-Analysis:**
- Summary estimate and precision (95% CI/credible interval)
- Measures of statistical heterogeneity (τ², I², prediction intervals)
- If other methods used: report synthesised result with measure of precision

**If Comparing Groups:**
- Direction of effect:
- Mean differences with 95% CI (if synthesising mean differences)
- Effect estimate (if expressed to different measure)

**If Investigating Heterogeneity:**
- Present results regardless of statistical significance
- If subgroup analysis:
  - Summary estimate within each subgroup
  - Estimate for difference between subgroups with precision
- If meta-regression:
  - Exact P value for regression coefficient with precision
  - Estimate for difference between subgroups with precision

**If Informal Methods for Heterogeneity:**
[Describe results observed]

**If Sensitivity Analyses:**
- Report results for each analysis
- Comment on robustness given results of corresponding sensitivity analyses

### Reporting Biases
[Present assessments of risk of bias due to missing results for each synthesis]
[If tool used: present responses to questions and judgements]
[If funnel plot generated: specify effect estimate and precision]
[If contour-enhanced funnel plot: specify milestones of statistical significance]
[If funnel plot asymmetry test: report exact P value]
[If sensitivity analyses: present results and compare with primary analysis]
[If studies assessed for selective non-reporting: consider presenting matrix with rows as studies and columns as syntheses]

### Certainty of Evidence
[Report overall certainty level for each important outcome]
[Provide explanation of reasons for rating down or up]
[Communicate certainty using appropriate format]
[Consider evidence summary tables like GRADE Summary of Findings]

## Discussion

### Interpretation
[Provide general interpretation of results in context of other evidence]

### Limitations of Evidence
[Discuss limitations of evidence]

### Limitations of Review Processes
[Discuss limitations of review processes and comment on potential impact]

### Implications
[Discuss implications for practice and policy]
[Make explicit recommendations for future research]

## Other Information

### Registration and Protocol

**Registration:**
- Register name and registration number:
- Or state review was not registered:

**Protocol:**
- Where protocol can be accessed (URL):
- Or state protocol was not prepared:

**Amendments:**
[Details of any amendments with rationale]

### Support
- Sources of financial or non-financial support:
- Relevant grant ID numbers:
- Role of funders/sponsors:

### Competing Interests
[Disclose authors' relationships or activities that could be perceived as pertinent]
[If authors had no competing interests, state this]

### Availability of Data, Code, and Other Materials
[Report which publicly available materials exist]
[If publicly available: report where they can be found]
[If available upon request: provide contact details and circumstances]

## Data & Code

**Data Availability:**

**Code Repository:**

**Search Strategies:**

**PRISMA Checklist:**

## References

1.
