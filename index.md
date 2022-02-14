## Welcome to GitHub Pages

### Dataset Overview
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
│   ├── participants.tsv
│   ├── participants.json
│   └── ...
└── ...
```

- `sourcedata`: data files directly from the sensor system
- `rawdata`: data files converted to BIDS data format
  - `sub-<label>`: for each subject a separate folder
  - `dataset_description.json`: describing the dataset
  - `participants.tsv`: demographics data of the study participants
  - `participants.json`: explaining each variable from the demographics data


Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Subject-specific Folders

Then, for each subject, the data are organized in a folder `sub-<label>`, with data from different recording modalities, *e.g.* EEG, IMU, etc., organized in a separate folder:
```markdown
.
├── sub-<label>/
├── eeg/
├── motion/
├── ...
└── sub-<label>_scans.tsv
```
Within each modality-specific folder, the data files are organized as follows:
```markdown
.
├── sub-<label>/
├── eeg/
├── motion/
│   ├── sub-<label>_task-<label>_tracksys-<label>_channels.tsv
│   ├── sub-<label>_task-<label>_tracksys-<label>_motion.tsv
└── ...
```
The data are stored in text-based format, and are `TAB` delimited. In this way, data can be read into MATLAB, Python, or even Excel.
