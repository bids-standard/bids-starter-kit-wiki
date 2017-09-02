Metadata are stored in .json and .tsv files. There are several ways to read and write these files.

# Reading and writing .json files

## Online
Go to http://jsoneditoronline.org/

## Matlab
Download a jsonread and write toolbox, an example of this is:
https://github.com/gllmflndn/JSONio

* Reading a .json file:
```matlab
    jsonread([filename])  
```

* Writing a .json file:
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

    % Assign the fields in the Matlab structure that can be saved as a json:
    anat_json.Manufacturer = 'GE';
    anat_json.ManufacturersModelName =  'Discovery MR750';
    anat_json.MagneticFieldStrength = 3;
    anat_json.PulseSequence = 'T1 weighted SPGR';

    json_options.indent = '    '; % this makes the json look pretier when opened in a txt editor
    jsonwrite(loc_json_name,loc_json,json_options)
```

# Reading and writing .tsv files

## Matlab
### Reading a .tsv file:

```matlab
    readtable([filename],'FileType','text','Delimiter','\t','TreatAsEmpty',{'N/A','n/a'});
```

### Writing a `.tsv` file: 
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
 
## Excel
* Create a file with the following columns (at least, for other values see... link to BIDS)
   * participant_id        
   * age 
   * sex
* Save as tab separated `.txt` and change extension to `.tsv`
 