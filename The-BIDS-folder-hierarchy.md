The BIDS format is essentially a particular way to structure your data / metadata within a hierarchy of folders. This makes it easy to browse from a computer, and makes minimal assumptions about the tools needed to interact with the data that's inside. These are the three main types of files you'll find in a BIDS dataset:

1. `.json` files that contain `key: value` metadata
2. `.tsv` files that contain tables of metadata
3. Raw data files (e.g., `.jpg` files for images or `.nii.gz` files for fMRI data.

These three types of files are organized into a hierarchy of folders that have specific naming conventions. The rest of this page describes how these folders are structured.

# Creating the BIDS Hierarchy
* BIDS hierarchy
    * `Project/Subject/Session/Acquisition`
    * Example: `myProject/sub-01/ses-01/anat/`
    * Project: can have any name
    * Subject: `sub-<participant label>`
    * Session: `ses-<session label>`
    * Acquisition: 'anat','fmri','dwi','meg','ieeg','eeg','derivatives','...' - this is the modality
 
# Starting with a subject
* Create a `<Project>/participants.tsv` file
* Create the `<Project>/<Subject>/<Session>/<Acquisition>` folder (e.g `myProject/sub-01/ses-01/anat/`)
 
## Which files go into the acquisition folder?
* **anat**: Anatomical MRI data in folder: `Project/sub-<>/ses-<>/anat/`
   * Data:  
      * `sub-<>_ses-<>_T1w.nii.gz`
   * Metadata:
      * `sub-<>_ses-<>_T1w.json`
 
* **fmri**: Functional MRI data in folder: `Project/sub-<>/ses-<>/func/`
   * TODO
 
* **meg**: MEG data in folder: Project/sub-<>/ses-<>/meg/
   * Data:
      * `sub-<>_ses-<>_task-<>_acq-<>_run-<>_proc-<>_meg.extension`
   * Metadata:
      * `sub-<>_ses-<>_task-<>_acq-<>_run-<>_proc-<>_meg.json`
   * Channel information:
      * `sub-<>_ses-<>_task-<>_acq-<>_run-<> _proc-<>_channels.tsv`
   * Events:
      * `sub-<>_ses-<>_task-<>_acq-<>_run-<> _proc-<>_events.tsv`
   * Sensor positions:
      * `sub-<>_ses-<>_acq-<>_photo.jpg`
      * `sub-<>_ses-<>_acq-<>_fid.json`
      * `sub-<>_ses-<>_acq-<>_fidinfo.txt`
      * `sub-<>_ses-<>_acq-<>_headshape.extension`
 
* **ieeg**: intracranial EEG data in folder: Project/sub-<>/ses-<>/ieeg/
   * Data:
      * `sub-<>_ses-<>_task-<>_acq-<>_run-<>_proc-<>_ieeg.extension`
   * Metadata:
      * `sub-<>_ses-<>_task-<>_acq-<>_run-<>_proc-<>_ieeg.json`
   * Channel information:
      * `sub-<>_ses-<>_task-<>_acq-<>_run-<> _proc-<>_channels.tsv`
   * Events:
      * `sub-<>_ses-<>_task-<>_acq-<>_run-<> _proc-<>_events.tsv`
   * Electrode locations:
      * `sub-<>_ses-<>_acq-<>_loc.json`               //coordinate metadata//
      * `sub-<>_ses-<>_acq-<>_loc.tsv `               //electrode xyz coordinates//
      * `sub-<>_ses-<>_acq-<>_locinfo.txt`            //freeform text//
      * `sub-<>_ses-<>_acq-<>_photo.jpg`              //operative photo//
 