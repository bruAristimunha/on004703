[![DOI](https://img.shields.io/badge/DOI-10.82901%2Fnemar.on004703-blue)](https://doi.org/10.82901/nemar.on004703)

CONTACT

For questions about this data set, please contact Anna Mai (anna.mai@mpi.nl; ORCiD 0000-0002-8343-9216). 

PERMISSIONS

These data may not be used for commericial purposes, including but not limited to use in any kind of training set for commercial machine learning applications.

These data may not be used in any way that either in part or in whole disambiguates participant identity, including but not limited to attempts at 3D facial reconstruction.

RECORDING SETUP

These data were collected from June 2018 to August 2019.

For all patients, a scalp electrode was used for referencing and ground. These were 13mm, 2.5M single lead subdermal electrodes made by Rochester Electro-Medical with serial number S81025-A-24RM.

Depth electrodes were manufactured by Ad-Tech and are Spencer Probe depth electrodes. Each electrode has 10 leads evenly spaced 3-7mm apart. 

With the exception of patients SD012 and SD022, all implants are depth electrodes. Patients SD012 and SD022 had grid and strip electrodes implanted in addition to several depth electrodes.

Any channel names beginning with ``C'' were not used and should be dropped from analyses.

TASK

Participants passively listened to 30-45s passages of conversational speech and  verbally answered a 2AC content question after each passage. 6 blocks with 7 passages per block.

MISSING DATA

Anatomical scans for particpant SD012 are not available due to excessive movement artifacts.

## Channel names follow the data headers (18 Oct 2026)

In 11 recordings the channel list of channels.tsv did not equal the data-file header (names, order or count), so `mne_bids.read_raw_bids` stopped with 'Channel mismatch' (or 'Duplicate channel names'); EEGDash renamed the data channels by position to the channels.tsv names, which gives wrong labels wherever the two lists are not aligned. Since 18 Oct 2026 every channels.tsv lists exactly the header channels, in header order, with the header names (MNE names: duplicated header labels numbered -0, -1).

Rows were matched to header channels BY NAME, never by position (exact; then case/whitespace; then the recorder prefix 'EEG '/'POL ', '_' and zero padding; then a trailing '-<reference>' token). Matched rows keep all their columns (type, units, status, ...); 0 rows took the header name.

10 header channels had no channels.tsv row (8 files) and got a new row: type from the name (ECG/EMG/EOG/trigger) or from the other contacts of the same shaft, else MISC; units from the header; status n/a. Examples: `sub-SD011_ses-01_task-PassiveListen_ieeg.edf`: Pleth; `sub-SD012_ses-01_task-PassiveListen_ieeg.edf`: Pleth; `sub-SD012_ses-02_task-PassiveListen_ieeg.edf`: Pleth.

17 channels.tsv rows had no channel in the data file (11 files) and were removed; they are kept verbatim under `sourcedata/channels-removed-2026-10-18/` (same relative path). Examples: `sub-SD010_ses-01_task-PassiveListen_ieeg.edf`: Trigger Event, Patient Event, STI 014; `sub-SD011_ses-01_task-PassiveListen_ieeg.edf`: STI 014; `sub-SD012_ses-01_task-PassiveListen_ieeg.edf`: STI 014.

EEGDash's positional renaming had given wrong labels to 773 channels in 9 files (rows missing, extra or out of order before that position).

## Negative event duration (18 Oct 2026)

In 5 events.tsv files one phoneme row had a negative duration (-16.351257 s; stimulus `s1503a-ex01`, word `virginia`, phone `ah`), the same in every subject, i.e. an error of the phoneme alignment of that stimulus. MNE refuses annotations with negative duration (`read_raw_bids` stopped with an AssertionError). The duration of that row is now `n/a`; onset and all other rows are unchanged. Files: `sub-SD011_ses-01_task-PassiveListen_events.tsv` (onset 2407.27965616 s), `sub-SD012_ses-02_task-PassiveListen_events.tsv` (onset 2316.57981631 s), `sub-SD019_ses-01_task-PassiveListen_events.tsv` (onset 2526.43596113 s), `sub-SD021_ses-01_task-PassiveListen_events.tsv` (onset 2462.68799463 s), `sub-SD022_ses-01_task-PassiveListen_events.tsv` (onset 2409.92375203 s).

## Electrode positions (20 Oct 2026)

Nine subjects (SD0xx with an `anat/*_contact_RAS.csv`) now have `sub-SDxxx_ses-01_space-Other_electrodes.tsv` and `..._coordsystem.json` (`Other`, `mm`). The x/y/z are the R/A/S columns of the deposit's own `anat/*_contact_RAS.csv` (one row per contact, name = label + contact number); they equal the authors' published MNI electrode coordinates. The deposit does not state which MNI template variant was used, so the frame is declared `Other` with that limitation in its description. Two recordings have no such file and remain without electrodes.
