---
layout: default
title: Home
rank: 1
---

# Minimal data standards
## Motivation
This page is intended as a blueprint for the data organization of all movement sensor-based projects of the [AG Neurogeriatrics](https://neurogeriatrics-kiel.com/de/). It should help to streamline analysis pipelines and keep projects organized for research partners.

## Folder Structure
The general folder structure for any dataset is depicted below:

```markdown
.
├── rawdata/
|   ├── dataset_description.json
│   ├── participants_overview.tsv
│   ├── participants_overview.json
│   ├── sub-<label>
│   |   ├── motion
│   ├── sub-<label>
│   └── ...
├── sourcedata/
├── scripts/
```
where:

- `rawdata`: data files converted to BIDS data format

  - `dataset_description.json`: describing the dataset with predefined fields in a [.json](https://neurogeriatricskiel.github.io/data/dataset_description.html) file.
  - `participants_overview.tsv`: [individual data](https://neurogeriatricskiel.github.io/data/participants.html) (demographic, clinical, ...) of the study participants which are session independent.
  - `participants_overview.json`: explaining each variable from the demographics data `participants_overview.tsv` file.
  - `participants_sessions.tsv`: individual data (demographic, clinical, ...) of the study participants change with each recorded session, only necessary if multiple sessions have been conducted
  - `participants_sessions.json`: explaining each variable from the demographics data `participants_sessions.tsv` file.
  - `sub-<label>`: separate folders for each subject
    - `motion`: folder containing all [motion related data](https://neurogeriatricskiel.github.io/data/motion.html). Can be extended to other modalities following the [BIDS standards](https://bids-specification.readthedocs.io/en/stable/)

- `sourcedata`: data files directly from the sensor system in most raw format avaliable
- `scripts`: self written software to bring source data into rawdata format

### Subject-specific Folders
Then, for each subject, the data are organized in a folder `sub-<label>`, with data from different recording modalities, *e.g.* EEG, motion, etc., organized in a separate folder:
```markdown
.
├── sourcedata/
├── rawdata/
    ├── sub-<label>
        ├── eeg/
        ├── motion/
        ├── ...
        └── sub-<label>_scans.tsv
```
Within each modality-specific folder, the data files are organized as follows:
```markdown
.
├── sourcedata/
├── rawdata/
    ├── sub-<label>
        ├── eeg/
        ├── motion/
            ├── sub-<label>_task-<label>_tracksys-<label>_channels.tsv
            ├── sub-<label>_task-<label>_tracksys-<label>_motion.tsv
            └── ...
        ├── ...
        └── sub-<label>_scans.tsv
```
The data are stored in text-based format, and are `TAB` delimited. In this way, data can be read into MATLAB, Python, or even Excel. However, if the files become too large, the user can change the file format *e.g.* .npy, but keeping the same tabular structure.

## File name structure
A filename consists of a chain of *entities*, or key-value pairs, a *suffix* and an
*extension*.
Two prominent examples of entities are `subject` and `session`.

For a data file that was collected in a given `session` from a given
`subject`, the filename MUST begin with the string `sub-<label>_ses-<label>`.
If the `session` level is omitted in the folder structure, the filename MUST begin
with the string `sub-<label>`, without `ses-<label>`.

Note that `sub-<label>` corresponds to the `subject` entity because it has
the `sub-` "key" and`<label>` "value", where `<label>` would in a real data file
correspond to a unique identifier of that subject, such as `01`.
The same holds for the `session` entity with its `ses-` key and its `<label>`
value.


## About
This page is maintained by [Robbin Johannes Romijnders](mailto:r.romijnders@neurologie.uni-kiel.de) and [Julius Welzel](mailto:j.welzel@neurologie.uni-kiel.de) in collaboration with Walter Maetzler and Clint Hansen.
