Welcome to the BIDS wiki

**Note: this wiki is under construction so the content may change quickly**

# Creating the BIDS Hierarchy
* BIDS hierarchy
    * `Project/Subject/Session/Acquisition`
    * Example: `myProject/sub-01/ses-01/anat/`
    * Project: can have any name
    * Subject: `sub-<participant label>`
    * Session: `ses-<session label>`
    * Acquisition: 'anat','fmri','dwi','meg','ieeg','eeg','derivatives','...' - this is the modality
 
# Starting with a subject
* Create a Project/participants.tsv file
* Create the Project/Subject/Session/Acquisition folder
 
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
 
# Creating a tsv file
Examples for the `particpants.tsv` file:
 
## Matlab
 
```
root_dir = 'MyRootDir';
bidsProject = 'temp';
bids_particpants_name = ['participants.tsv'];
 
participant_id = ['sub-01'; 'sub-02']; % onsets in seconds
age = [20 30]';
sex = ['m';'f'];
 
t = table(participant_id,age,sex);
writetable(t,fullfile(root_dir,bidsProject,bids_particpants_name),'FileType','text','Delimiter','\t');
```
 
## Excell
* Create a file with the following columns (at least, for other values see... link to BIDS)
   * participant_id        
   * age 
   * sex
* Save as tab separated .txt and change extension to .tsv
 
# Creating a json file
 
* Matlab:
   * Download a jsonread and write toolbox, an example of this is:
      * https://github.com/gllmflndn/JSONio
   * Now, you can use this code to create a template structure and save a json file

```matlab
root_dir = './';
project = 'temp';
sub_id = '01';
ses_id = '01';
acquisition = 'anat';
 
anat_json_name = fullfile(root_dir,project,...
    ['sub-' sub_id],...
    ['ses-' ses_id],...
    acquisition,...
    ['sub-' sub_id '_ses-' ses_id '_T1W.json']);
 
% these fields are required:
% FIGURE THIS OUT FOR ANATOMY FILES
 
% these fields are optional:
anat_json.Manufacturer = 'GE';
anat_json.ManufacturersModelName =  'Discovery MR750';
anat_json.MagneticFieldStrength = 3;
anat_json.PulseSequence = 'T1 weighted SPGR';
 
jsonwrite(anat_json_name,anat_json)
```
 
# Reading a tsv file
 
## Matlab:

```matlab
readtable([filename],'FileType','text','Delimiter','\t');
```
 
# Reading a json file
Download a jsonread and write toolbox, an example of this is:
https://github.com/gllmflndn/JSONio

## Matlab
```matlab
jsonread([filename])
```