## What is a BIDS App?

A BIDS App is an analysis pipeline that takes a BIDS formatted dataset as input and has all of its dependencies packaged within a container ([Docker](https://www.docker.com/) or [Singularity](https://singularity.lbl.gov/))

## Helpful Links

[Example BIDS App repository](https://github.com/BIDS-Apps/example) : A minimalist example of a BIDS App consisting of a Dockerfile and a simple entry point script (written in this case in Python) accepting the standard BIDS Apps command line arguments. This repository can be used as a template for new BIDS Apps.

## FAQ

**Which container do I use to start building my BIDS App?**

The only minimum requirements of a BIDS App's container is its ability to
run your pipeline. So for example, if your app is mostly Python based it should be sufficient to start
with any image that has Python and include your pipenv dependencies.

<br>

**I noticed that every BIDS app follows some specific arguments such as `bids_dir`, `output_dir`, and `analysis_level` and `participant_label`. Can I add more arguments?**

Yes, the mandatory arguments that you have listed should be in every BIDS App, but 
you are free to add more that are specific to the task your app will perform.

<br>

**I noticed that there are 2 kinds of analysis levels --> `participant` and `group`. What does this mean?**

Generally, "participant" means individual level analysis (i.e. single subject)
The group level analysis can be thought of as the second step, where the input becomes
the output of the "participant" level analysis.
For example, generating statistic maps of each subject's brain could be considered "participant",
while generating the average of these maps across the dataset could be considered "group".

**What do we do if our application does not have any use for the group level analysis?**

If your pipeline has no need for group level analysis, it is fine if it is only valid
for the analysis_level argument (see [fmriprep](http://fmriprep.readthedocs.io/en/latest/usage.html))

<br>

**Is it mandatory to first check the dataset validity using the BIDS-validator?**

It is an extremely helpful feature to have validation of the dataset as part of your tool. However, it's not considered mandatory. (i.e. I know of many apps that just simply fail with an error message if the dataset is not BIDS compliant)