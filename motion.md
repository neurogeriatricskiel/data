---
layout: default
title: motion\
rank: 4
---
## Motion specific data (`motion\`)
Within each motion specific folder, the data files are organized as follows:
```markdown
.
├── sourcedata/
├── rawdata/
    ├── sub-<label>
        ├── motion/
            ├── sub-<label>_task-<label>_tracksys-<label>_channels.tsv
            ├── sub-<label>_task-<label>_tracksys-<label>_motion.tsv
            └── ...
        ├── ...
        └── sub-<label>_scans.tsv
```
The data are stored in text-based format, and are `TAB` delimited. In this way, data can be read into MATLAB, Python, or even Excel. However, if the files become too large, the user can change the file format *e.g.* .npy, but keeping the same tabular structure. The full template would read as follows (`[]` means optional): <br>
`sub-<label>[_ses-<label>][_task-<label>][_run-<index>][_tracksys-<label>]_motion.*`


## Channels description (`*_channels.tsv`)
```
└─ sub-<label>\
    └─ \[ses-<label>]\
        └─ motion\
            └─ sub-<label>[_ses-<label>][_task-<label>][_tracksys-<label>]_channels.tsv
```
This file is REQUIRED as it makes it easy to browse or query over larger collections of datasets. The REQUIRED columns are channel `name`, `type`, `tracked_point`, `tracking_system`, `component` and `unit`. Any number of additional columns may be added to provide additional information about the channels.

The columns of the channels description table stored in `*_channels.tsv` are:

MUST be present:

| **Key name**    | **Requirement level** | **Data type** | **Description**                                                                                                                                                                                                     |
| --------------- | --------------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| name            | REQUIRED              | string        | Label of the channel. Entries have to match headers in (any) `*_motion.tsv.`                                                                                                                                        |
| tracked_point   | REQUIRED              | string        | Label of the point that is being tracked, for example, label of a tracker or a marker (“LeftFoot”, “RightWrist”).                                                                                                   |
| type            | REQUIRED              | string        | Type of data.                                                                                                                                                                                                       |
| component       | REQUIRED              | string        | Component of the representational system described in `*_coordinatesystem.tsv` that the channel contains.                                                                                                           |
| units           | REQUIRED              | string        | Physical unit of the value represented in this channel, for example, vm for virtual meters, radian or degrees for angular quantities. See the BIDS spec for guidelines for Units and Prefixes.                      |
| sampling_frequency           | REQUIRED              | number        | Nominal sampling rate of the channel in Hz.                       |


SHOULD be present:

| **Key name** | **Requirement level** | **Data type** | **Description**                                                                                                                                                            |
| ------------ | --------------------- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| placement    | RECOMMENDED           | string        | Placement of the tracked point on the body (for example, participant, avatar centroid, torso, left arm). It can refer to an external vocabulary for describing body parts. |
| description  | OPTIONAL              | string        | Brief free-text description of the channel, or other information of interest.                                                                                              |

Restricted keyword list for column `type` in alphabetic order (shared with the other BIDS modalities?). Note that upper-case is REQUIRED:

| **Keyword**  | **Description**                  |
| ------------ | -------------------------------- |
| ACC          | Acceleration                     |
| ANGACC       | Angular acceleration             |
| ANGVEL       | Angular velocity                 |
| ORNT         | Orientation                      |
| POS          | Position in space                |
| VEL          | Velocity                         |
| *TIMESTAMPS* | *Timestamps of recorded samples* |

Restricted keyword list for column `component` in alphabetic order (shared with the other BIDS modalities?). Note that upper-case is REQUIRED:

| **Keyword** | **Description**         |
| ----------- | ----------------------- |
| x           | entity along the X-axis |
| y           | entity along the Y-axis |
| z           | entity along the Z-axis |

Example `channels.tsv`:

```Text
name		  tracked_point		type	    component	     units      sampling_frequency
t1_acc_x	  LeftFoot	        ACC	        x		         m/s^2      200
t1_acc_y	  LeftFoot	        ACC	        y		         m/s^2      200      
t1_acc_z	  LeftFoot	        ACC	        z		         m/s^2      200
t1_gyro_x	  LeftFoot	        ANGVEL	    x		         rad/s      200
t1_gyro_y	  LeftFoot	        ANGVEL	    y		         rad/s      200
t1_gyro_z	  LeftFoot	        ANGVEL	    z		         rad/s      200
```
