---
layout: default
title: participants_*
rank: 3
---

## Participants overview file (`participants_overview*`)

Template:

```Text
participants_overview.tsv
participants_overview.json
```
The purpose of this RECOMMENDED file is to describe properties of participants which are session independent such as age, sex, handedness and so forth. If this file exists, it MUST contain the column participant_id, which MUST consist of sub-<label> values identifying one row for each participant, followed by a list of optional columns describing participants. Each participant MUST be described by one and only one row.

`participants_overview.tsv` example:

```Text
participant_id  sex   handedness  group
sub-01          M     right       patient
sub-02          F     right       control
sub-03          F     n/a         patient
```
It is RECOMMENDED to accompany each `participants_overview.tsv` file with a sidecar `participants_overview.json` file to describe the TSV column names and properties of their values (see also the section on tabular files). Such sidecar files are needed to interpret the data, especially so when optional columns are defined beyond age, sex, handedness, such as group in this example, or when a different age unit is needed (for example, gestational weeks).

`participants_overview.json` example:
```Text
{
    "sex": {
        "Description": "sex of the participant as reported by the participant",
        "Levels": {
            "M": "male",
            "F": "female"
        }
    },
    "handedness": {
        "Description": "handedness of the participant as reported by the participant",
        "Levels": {
            "left": "left",
            "right": "right"
        }
    },
    "group": {
        "Description": "group the participant belonged to",
        "Levels": {
            "control": "participants who have been assigned to a control condition",
            "patient": "participants who have been assigned to a experimental condition"
        }
    }
}
```
## Participants session file (`participants_session*`)

Template:

```Text
participants_session.tsv
participants_session.json
```
The purpose of this RECOMMENDED file is to describe properties of participants which are session dependent such as age, weight, clinical score (e.g. MDS-UPDRS-III) and so forth. If this file exists, it MUST contain the column participant_id, which MUST consist of sub-<label> values session_id and identifying one row for each participant per visit, followed by a list of optional columns describing participants.

`participants_overview.tsv` example:

```Text
participant_id  session_id  age weight  MDS-UPDRS-III
sub-01          BL          35  72      65
sub-01          FU1         41  75      42
sub-02          BL          55  64      78
```
For the same reasons as mentioned above, it is RECOMMENDED to have a accompanied `participants_overview.json` file.

`participants_overview.json` example:
```Text
{
    "session_id": {
        "Description": "Label of sessions conducted",
        "Levels": {
            "BL": "Session within 3 weeks prior to intervention",
            "FU1": "Follow-up after 6-9 month after intervention"
        },
    "age": {
            "Description": "age of the participant",
            "Units": "years"
        },
    "MDS-UPDRS-III": {
        "Description": "MDS-UPDRS-III total score of the participant",
        "Units": "Total points, range 0-144"
    }
}
```
