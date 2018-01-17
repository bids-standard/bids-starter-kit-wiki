Metadata are stored in .json and .tsv files. These files are language-agnostic, meaning you
can work with them in, e.g., Python, Matlab, or R. This page covers common ways to read/write
these files in common languages for neuroscience analysis.

# JSON Files
JSON files are text files that take the following structure:
`{'key': 'value', 'key2': 'value2', 'key3': {'subkey1': 'subvalue1'}}`.

Note that they can be nested (curly brackets within curly brackets). Here are some
common ways to read / write these files.

## Online
To read/write JSON online, we recommend the following website:

http://jsoneditoronline.org/

## Matlab
There are many toolboxes in Matlab for reading / writing JSON files. One
example is:

https://github.com/gllmflndn/JSONio

### Reading a `.json` file
```matlab
    jsonread([filename])  
```

### Writing a `.json` file
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
    jsonwrite(loc_json_name,anat_json,json_options)
```
## Python
In Python, JSON support is built into the core library, meaning you don't need to install anything
to read/write JSON files. In addition, the structure of JSON is almost identical to that of
Python dictionaries (assuming you are only storing text / numbers in the dictionary). To that
extent.

### Reading a `.json` file
```python
import json
with open('myfile.json', 'r') as ff:
    data = json.load(ff)
```

### Writing a `.json` file
```python
import json
data = {'field1': 'value1', 'field2': 3, 'field3': 'field3'}
with open('my_output_file.json', 'w') as ff:
    json.dump(data, ff)
```

## R
There are several packages for reading and writing JSON files from R. In this example, we will be using jsonlite. Remember to install and call a package before using it.

https://github.com/jeroen/jsonlite

### Installing required package
```R
    install.packages('jsonlite')
```

### Reading a `.json` file:
```R
    library(jsonlite)
    data = fromJSON('myfile.json', pretty=TRUE)
```

### Writing a `.json` file:
```R
    library(jsonlite)
    data = '{"field1": "value1", "field2": 3, "field3": "field3"}'
    writeLines(data, file="myData.json")
```



# TSV files
A Tab-Separate Values (TSV) file is a text file where tab characters (`\t`) separate
fields that are in the file. It is structured as a table, with each column representing
a field of interest, and each row representing a single datapoint.

Below are ways to read / write TSV files in common languages.

## Matlab
### Reading a `.tsv` file:

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

## Python
In Python, the easiest way to work with TSV files is to use the Pandas library. This provides a high-level
structure to organize, manipulate, clean, and visualize tabular data. You can install `pandas` with the
following command:

`pip install pandas`

### Reading a `.tsv` file
There are many ways to read a `.tsv` file in Pandas. One option is the following:

```python
import pandas as pd
pd.read_csv('./ds001/participants.tsv', delimiter='\t')
```
Note that this function will default to using `,` as a delimiter, so we explicitly give it the tab character.

### Writing a `.tsv` file
You can write to a `.tsv` file using the `to_csv` method of a pandas DataFrame:

```python
import pandas as pd
df = pd.read_csv('./ds001/participants.tsv', delimiter='\t')

# Add an extra column for demonstration
df['subject_id'] = range(len(df))

# Show contents of the dataframe
df.head()
    Out:
          participant_id sex  age  subject_id
    0         sub-01   F   26           0
    1         sub-02   M   24           1
    2         sub-03   F   27           2
    3         sub-04   F   20           3
    4         sub-05   M   22           4

# Save as a CSV file
df.to_csv('my_new_file.csv', sep='\t')
```

## Excel
* Create a file with the following columns (at least, for other values see paragraph 8.11 in [BIDS spec 1.0.2](http://bids.neuroimaging.io/bids_spec1.0.2.pdf))
   * participant_id        
   * age 
   * sex
* Save as tab separated `.txt` and change extension to `.tsv`
 
## R
Reading and writing tab separated files comes natively in R, no need for extra packages.

### Reading a `.tsv` file:
In this example, we assume the .tsv includes column names (headers), and explicitly set column separator (delimitor) to tab ('\t')
```
data = read.table('myFile.tsv', header=TRUE, sep='\t')
```

### Writing a `.tsv` file:
When writing files, column and row names are always saved, we remove row names, and quotes from the outpur explicitly by setting them to FALSE.

```R
data = cbind.data.frame(
  participant_id = c('sub-01', 'sub-02'),
  age = c(20,30),
  sex = c('m','f'))

write.table(data, file='myData.tsv',sep='\t',
  row.names = FALSE, quote = FALSE)
```