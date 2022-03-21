# Minimal data standards
## Motivation
This page is intended as a blueprint for the data organization of all sensor-based projects of the [AG Neurogeriatrics](https://neurogeriatrics-kiel.com/de/). It should help to streamline analysis pipelines and keep projects organized for research partners.

## Folder Structure
The general folder structure for any dataset is depicted below:

```markdown
.
├── sourcedata/
├── rawdata/
│   ├── sub-<label>
│   ├── sub-<label>
│   ├── ...
│   ├── sub-<label>
│   ├── dataset_description.json
│   ├── participants_overview.tsv
│   ├── participants_overview.json
│   └── ...
└── ...
```
where:
- `sourcedata`: data files directly from the sensor system
- `rawdata`: data files converted to BIDS data format
  - `sub-<label>`: for each subject a separate folder
  - `dataset_description.json`: describing the dataset
  - `participants_overview.tsv`: demographics data of the study participants
  - `participants_overview.json`: explaining each variable from the demographics data

### Subject-specific Folders
Then, for each subject, the data are organized in a folder `sub-<label>`, with data from different recording modalities, *e.g.* EEG, IMU, etc., organized in a separate folder:
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

## About
This page is maintained by [Robbin Johannes Romijnders](mailto:r.romijnders@neurologie.uni-kiel.de) in collaboration with Walter Maetzler and Clint Hansen.
