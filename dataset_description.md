---
layout: default
title: dataset_description.json
rank: 2
---

## Dataset description (`dataset_description.json`)
The file `dataset_description.json` is a JSON file describing the dataset. Every dataset MUST include this file with the following fields:

| **Key name** | **Requirement level** | **Data type** | **Description**                                                                                                                                                                                   |
| ------------ | --------------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Name     | REQUIRED              | string        | Name of the dataset. |

Generic fields SHOULD be present: For consistency between studies and institutions, we
encourage users to extract the values of these fields from the actual raw data.
Whenever possible, please avoid using ad hoc wording.

| **Key name**                | **Requirement level** | **Data type** | **Description**                                                                                     |
| --------------------------- | --------------------- | ------------- | --------------------------------------------------------------------------------------------------- |
| License          | RECOMMENDED           | string        | The license for the dataset. The use of license name abbreviations is RECOMMENDED for specifying a license.     |
| Authors | RECOMMENDED           | array of strings        | List of individuals who contributed to the creation/curation of the dataset. |
| Funding             | RECOMMENDED           | array of strings        | List of sources of funding (grant numbers).       |
| EthicsApprovals                | RECOMMENDED           | array of strings        | List of ethics committee approvals of the research protocols and/or protocol identifiers.                                |                
