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
The data are stored in text-based format, and are `TAB` delimited. In this way, data can be read into MATLAB, Python, or even Excel. However, if the files become too large, the user can change the file format *e.g.* .npy, but keeping the same tabular structure.

## Channels description (`*_channels.tsv`)

└─ sub-<label>\
└─ \[ses-<label>]\
└─ motion\
└─ sub-<label>\[\_ses-<label>][\_task-<label>\]_channels.tsv

This file is REQUIRED as it makes it easy to browse or query over larger collections of datasets. The REQUIRED columns are channel `name`, `type`, `tracked_point`, `tracking_system`, `component` and `unit`. Any number of additional columns may be added to provide additional information about the channels.

The columns of the channels description table stored in `*_channels.tsv` are:

MUST be present:

| **Key name**    | **Requirement level** | **Data type** | **Description**                                                                                                                                                                                                     |
| --------------- | --------------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| name            | REQUIRED              | string        | Label of the channel. Entries have to match headers in (any) `*_motion.tsv.`                                                                                                                                        |
| tracked_point   | REQUIRED              | string        | Label of the point that is being tracked, for example, label of a tracker or a marker (“LeftFoot”, “RightWrist”).                                                                                                   |
| tracking_system | REQUIRED              | string        | Label of the tracking system the channel belongs to. Entry has to correspond to one of the entries in field `TrackingSystems` in `*_motion.json` and labels in key-value pair `*[_tracksys_<label>]` in file names. |
| type            | REQUIRED              | string        | Type of data.                                                                                                                                                                                                       |
| component       | REQUIRED              | string        | Component of the representational system described in `*_coordinatesystem.tsv` that the channel contains.                                                                                                           |
| units           | REQUIRED              | string        | Physical unit of the value represented in this channel, for example, vm for virtual meters, radian or degrees for angular quantities. See the BIDS spec for guidelines for Units and Prefixes.                      |

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
| X           | entity along the X-axis |
| Y           | entity along the Y-axis |
| Z           | entity along the Z-axis |

Example `channels.tsv`:

```Text
name		    tracked_point	  tracking_system	 type	    component	  units
t1_acc_x	  LeftFoot	      IMU1acc		       ACC	    x		         m/s^2
t1_acc_y	  LeftFoot	      IMU1acc		       ACC	    y		         m/s^2
t1_acc_z	  LeftFoot	      IMU1acc		       ACC	    z		         m/s^2
t1_gyro_x	  LeftFoot	      IMU1gyro	       ANGVEL	  x		         rad/s
t1_gyro_y	  LeftFoot	      IMU1gyro	       ANGVEL	  y		         rad/s
t1_gyro_z	  LeftFoot	      IMU1gyro	       ANGVEL	  z		         rad/s
…
t2_acc_x	  RightWrist 	    IMU2		         ACC	    x		         m/s^2
t2_acc_y	  RightWrist	    IMU2		         ACC	    y		         m/s^2
t2_acc_z	  RightWrist	    IMU2		         ACC	    z            m/s^2
t2_gyro_x   RightWrist	    IMU2		         ANGVEL	  x	           rad/s
…
m1_pos_x	  LeftThigh	     OPTpos		         POS	    x		        m
m1_pos_y	  LeftThigh	     OPTpos		         POS	    y		        m
m1_pos_z	  LeftThigh	     OPTpos		         POS	    z		        m

```
