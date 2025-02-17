# Data Reuse and Author Career Dynamics: An Analysis Based on ICPSR, SciSciNet, and OpenAlex

This repository hosts datasets created from publications that cite ICPSR datasets (source: https://github.com/ICPSR/mica-data-descriptor/tree/main). These datasets have been cross-referenced with OpenAlex and SciSciNet to include only those publications that:
- Cite ICPSR datasets,
- Possess a DOI, and
- Have valid identifiers in either SciSciNet or OpenAlex (for both publications and authors).

Below is a concise description of each dataset provided.

---

## 1. ICPSR Publications Data

### `icpsr_publications.csv`
This dataset contains publication records from the original **106,403** ICPSR publications. Among these, only those publications with a valid identifier in either SciScinet or OpenAlex were retained—resulting in a total of **36,526** unique publications (based on REF_ID).

In this dataset, if a publication has multiple authors, each author is expanded into an individual record—resulting in a total row count that exceeds **36,526** and comprising **15,733** unique authors.

**Key Variables:**
- **REF_ID:** Unique publication identifier (from ICPSR).
- **DOI:** Digital Object Identifier for the publication.
- **Title:** Title of the publication.
- **Paper_ID:** Unique paper identifier (default is from SciScinet; if unavailable, OpenAlex is provided).
- **Author:** Name of the publication author.
- **Author_ID:** Identifier(s) for the author from SciScinet and OpenAlex.
- **STUD_NUMS, SERIES_NUMS:** ICPSR study and series numbers cited by the publication.
- **YEAR_PUB:** Year of publication.
- **Affiliation_ID:** Identifier(s) for the author's affiliation from SciScinet and OpenAlex.
- **Author_Sequence_Number:** Position of the author in the publication's author list.
- **Total_Authors:** Total number of authors on the publication.

---

~~## 2. Publication Bibliography~~

~~### `publications_bibliography.csv`~~

~~This file provides detailed bibliographic metadata for the 29,326 publications that meet the filtering criteria. It includes information such as citation counts, topics, fields, and domains.~~

~~**Key Variables Include:**~~  
~~- **Ref_Id, Doi, OpenAlex_ID**~~  
~~- **Cited_By_Count**~~  
~~- **Authors, Institutions**~~  
~~- **Primary_Topic_ID, Primary_Topic_Display_Name**~~  
~~- **Topics_IDs, Topics_Display_Names**~~  
~~- **Subfield_ID, Subfield_Display_Name**~~  
~~- **Field_ID, Field_Display_Name**~~  
~~- **Domain_ID, Domain_Display_Name**~~

**Note:** Section 2 requires revision.

---

## 3. Author Information

### `icpsr_publication_authors_info.csv`
This dataset contains a unique list of publication authors who have cited an ICPSR study or series, along with detailed metadata about their research careers.

**Key Variables:**
- **Author:** The name of the publication author who cited an ICPSR study or series.
- **Author_ID:** The unique identifier for the author. The default identifier is from SciScinet; however, in cases where the SciScinet ID is not available, the OpenAlex ID is provided. When multiple IDs exist, they are separated by semicolons (`;`).
- **Unique_PaperIDs:** A semicolon-separated list of unique paper identifiers representing the publications in which the author has participated. This list includes not only publications that cite the ICPSR dataset but also other publications.
- **Unique_PaperIDs_Count:** The total number of unique papers listed in **Unique_PaperIDs**.
- **Min_Year:** The earliest publication year among the author's works.
- **Max_Year:** The most recent publication year among the author's works.
- **Research_Duration:** The span of years between **Min_Year** and **Max_Year**, indicating the duration of the author's research activity.
- **H-index:** A metric that reflects the author's research impact based on both the productivity and citation impact of their publications.
- **Dataset_PI:** A dummy variable (1 or 0) indicating whether the author appears as a principal investigator (PI) in any ICPSR study or series. In this dataset, **157** authors are flagged as PI.
- **STUDY_PI_NUMBER:** A semicolon-separated list of study numbers (STUD_NUMS) for which the author is identified as the PI in the study dataset.
- **SERIES_PI_NUMBER:** A semicolon-separated list of series numbers (SERIES_NUMS) for which the author is identified as the PI in the series dataset.
---

## 4. Indirect Data Citation Networks

### a. `author_indirect_datacitation_pairs.csv`
This file captures indirect citation relationships between authors who are not coauthors but have independently cited the same ICPSR dataset. Although the dataset contains **43,929,587** total citation pair records, the number of unique author pairs is **3,938,655**. In this context, **shared_study_series_num** is a core variable indicating which ICPSR study/series number(s) were cited by the publications to establish the indirect citation relationship.

**Key Variables:**
- **author_1, author_2:** The pair of authors involved in the indirect citation relationship. These pairs are undirected (order does not matter) and are always listed in alphabetical order.
- **source_REF_ID, target_REF_ID:** The ICPSR publication identifiers for the citing publications (source and target, respectively).
- **source_YEAR_PUB, target_YEAR_PUB:** The publication years for the corresponding source and target publications.
- **shared_study_series_num:** The specific ICPSR study/series number(s) cited by each publication that links the author pair.
- **author1_author_id, author2_author_id:** The author identifiers corresponding to **author_1** and **author_2**, respectively.
- **author1_affiliation_id, author2_affiliation_id:** The institution identifiers for **author_1** and **author_2**, respectively.
- **affiliation_match:** A dummy variable indicating whether the affiliation information for the publication is complete; if either author's institution information is missing (i.e., NaN) for that publication, this value is NaN. In this dataset, the non-null ratio for this variable is **52.96%**; among non-null entries, **98.53%** have a value of 0 and **1.47%** have a value of 1.
- **source_total_authors, target_total_authors:** The total number of authors on the source and target publications, respectively.
- **historical_affiliation_match:** A dummy variable computed by comparing the entire affiliation history of the author; if at least one affiliation matches across their publication history, this value is 1, otherwise it is NaN if any affiliation information is missing. The non-null ratio for this variable is **89.06%**; among non-null entries, **82.99%** have a value of 0 and **17.01%** have a value of 1.

~~### b. `author_data_indirect_citation_pairs_summary.csv`~~  
~~This summary dataset aggregates indirect citation information for each author, providing an overview of their citation connections.~~  

~~**Data Structure:**~~  
~~- **author_id:** Unique identifier for an author~~  
~~- **Total_Unique_REF_IDs:** Count of unique publication REF_IDs associated with the author~~  
~~- **Unique_REF_IDs:** List of unique publication REF_IDs (stored as an object)~~  
~~- **sum_unique_nums:** Sum of unique numbers across references (aggregated metric)~~  
~~- **Total_Unique_STUD_NUMS:** Count of unique ICPSR study numbers cited by the author~~  
~~- **Unique_STUD_NUMS:** List of unique study numbers (with some missing values)~~  
~~- **Total_Unique_SERIES_NUMS:** Count of unique ICPSR series numbers cited~~  
~~- **Unique_SERIES_NUMS:** List of unique series numbers (partial data)~~  
~~- **Total_Indirect_Connections:** Total number of indirect citation connections for that author~~  
~~- **Indirect_Authors:** List of indirectly connected authors (present in a subset of records)~~  

~~*Data Shape:* 9,763 entries, with 10 columns in total.~~

**Note:** Section 4.b requires revision.
---

~~## 5. Coauthor Pairs~~

~~### `coauthor_pairs.csv`~~  
~~This dataset lists pairs of authors who have coauthored publications. It is derived from the complete set of publication records by authors who have published works citing ICPSR datasets, meaning it encompasses all publication data from these authors.~~

~~**Key Variables:**~~  
~~- **author_1, author_2:** The pair of coauthors~~  
~~- **shared_work_id:** Identifier for the shared publication that both authors contributed to~~  
~~- **publication_year:** Year in which the shared publication was released~~

~~---~~

~~## 6. Future and Prior Coauthorships~~

~~### a. `future_coauthorships.csv`~~  
~~This file identifies author pairs that did not have an established coauthorship relationship initially but later coauthored publications following an indirect citation link.~~

~~**Key Variables:**~~  
~~- **author_1, author_2**~~  
~~- **source_REF_ID, target_REF_ID**~~  
~~- **source_YEAR_PUB, target_YEAR_PUB**~~  
~~- **shared_study_series_num:** Core variable indicating the specific ICPSR study/series numbers cited by each publication, establishing the indirect citation link~~  
~~- **max_YEAR_PUB:** The latest publication year among the pair~~  
~~- **source_target:** Directional citation indicator~~  
~~- **shared_work_ids:** List of shared publication IDs~~  
~~- **publication_years:** Years of the publications~~

~~*Unique Future Coauthorships:* **5,464 pairs** (0.34% of all unique author pairs)~~  
~~*Unique authors in future collaborations:* **3,259 authors** (34.3% of all authors)~~

~~### b. `prior_coauthorships.csv`~~  
~~This dataset contains author pairs that were already established as coauthors.~~

~~### c. `non_coauthorships.csv`~~  
~~This file lists author pairs that never coauthored publications, either before or after the indirect citation event.~~

~~**Summary Statistics for Indirect Citation Pairs:**~~  
~~- **Future Coauthorships:** 5,464 (0.34%)~~  
~~- **Prior Coauthorships:** 11,605 (0.71%)~~  
~~- **Non-Coauthorships:** 1,612,169 (98.95%)~~  
~~- **Total Unique Author Pairs:** 1,629,238~~

**Note:** Section 5 and 6 requires revision.
---
