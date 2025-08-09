# 🚗 Automotive Review Crew: A Parallel and Sequential Agent Workflow

This project demonstrates a multi-agent system built with the `crewai` framework to perform a comprehensive automotive review. It showcases an efficient workflow that combines parallel data collection with sequential synthesis to deliver a single, unbiased report.

## 🚀 How It Works

The workflow is a two-step process designed to gather and synthesize information quickly and effectively:

### 1. Parallel Information Gathering

Three reviewer agents (`reviewer1`, `reviewer2`, `reviewer3`) are assigned to search specific automotive websites (Edmunds, Car and Driver, Top Gear) for a given topic. These tasks run **simultaneously** to gather information efficiently.

**Why this is beneficial:** Instead of manually visiting each site one by one, these agents perform the searches in parallel. This significantly speeds up the information collection process and ensures that we get a broad, non-biased view by consulting multiple sources at once.

### 2. Sequential Synthesis

After the three reviewers have completed their work, a fourth agent (`synthesizer`) takes their combined outputs as context. This task runs **sequentially**, as it depends on the completion of the previous three. The synthesizer agent then creates a final report that includes:

* A list of consensus points.
* A final verdict for buyers.
* Highlights of where the reviewers agree and disagree.

**Why this is beneficial:** The synthesizer's job is to reconcile differing opinions and extract a single, objective summary. This prevents the user from having to read through three separate, potentially biased reports. The final output is a clean, non-redundant, and comprehensive report ready for immediate use.

