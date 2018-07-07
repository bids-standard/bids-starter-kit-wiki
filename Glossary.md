# BIDS jargon busting

<img align="right" width="35%" src="https://imgs.xkcd.com/comics/period_speech.png" alt="XKCD comic 771"/>

***Simple definitions for any BIDS related terms***

We know that when you're getting started with something new there are often jargon-y words that make understanding everthing that's going on kinda hard.

The point of this list is to give you a place to go to figure out some of those terms that "everyone" seems to know.

Please add to this list! It will always be :construction: **in construction** :construction: and we really encourage everyone to update it to be more useful. If there's a word you don't know, there's almost certainly someone else who doesn't know what it means either.

**If you are unsure about a term/definition that you are adding, please add it anyway and add an asterix(*) to signal that you want it reviewed.**

### General resources

We aren't covering all words associated with brain imaging (that might be rather overwhelming) so we're also collecting together some more general resources here:

* MIT Brain Research's glossary of brain imaging terminology: http://mindhive.mit.edu/node/71

### BIDS Terms

#### 0-9

#### A
* **acquisition**: one continuous block of a scan

#### B
* **BIDS**: Brain Imaging Data Structure - a standardised way to organise your neuroimaging data.
  * http://bids.neuroimaging.io

#### C
* **container**: A container is a file which packages all the software and instructions required to perform a series of tasks. 

#### D
* **derivatives**: processed (i.e. non-raw) data
* **dataset**: a collection of data that can include many subjects or sessions

#### E
* **extensions**: branches of BIDS that are for specific types of data (i.e. PET)

#### F
* **file extension**: A file extension is the suffix following the last `.` in a filename, for example the `.jpeg` in `dog.jpeg`. These exist to give us instructions on how to interpret files. File extensions that are important in BIDS are [`.json`](#j), `.nii`, [`.tsv`](#t)

#### G

#### H
* **heuristic file**: a file that can sort your data into categories based on naming patterns

#### I

#### J
* **JSON**: A JSON file can be though of as a form or as a list of name value pairs. Example: {"firstName": "John", "lastName": "Smith"}.

#### K

#### L
* **library*: 

#### M
* **metadata*: Supporting data that describes your main data (i.e. data about data). For example if your main data is an MRI image your metadata might be information about the date and time of imaging, the image type, the machine serial number etc.
  * An example: "Scan Date" would be metadata that describes your actual data (Neuroimaging scans) 

#### N

#### O
* **open science**: Scientific research and data that is free and available for everyone to use

#### P
* **parameter**: generally speaking, a parameter is numerical variable that we (scientists, computer programs, etc) are able to manipulate in order to change outcomes.

#### Q

#### R
* **README**: A readme is a text file. The readme's purpose is to provide explanation and documentation for the contents of the folder it lives in.

#### S
* **subject**: a person / animal / object participating in a study

* **session**: 

* **sequence**: 

* **sidecar* (as in json sidecar): A json file associated to a nii file (usually by having the same name preceding the [file extension](#f)). Together these make up an acquisition; the nii file contains the image and the json contains various [metadata](#m).

#### T
* **tsv*: tsv stands for **t**ab **s**eparated **v**alues. A .tsv file contains a table (like a simple excel spreadsheet) containing text. Table values are separated by tabs.

#### U

#### V


#### W

#### X

#### Y

#### Z
