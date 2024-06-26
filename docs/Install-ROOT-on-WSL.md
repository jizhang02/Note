# Insatall ROOT on WSL
### Preface
#### 🧐 What is ROOT?
ROOT is a general data analysis framework developed by CERN. It is an object-oriented framework for storing, processing and visualizing large scientific data sets. ROOT can be used in a variety of scientific fields, including physics, astrophysics, biology, medicine, and more.
#### 🧐 What is SNAP?
In Linux, snap is a software package format developed by Ubuntu. Snap packages are self-contained, which means they contain all files and dependencies required by the application. This makes them easier to install and use, and more secure because they don't rely on other software on the system.

Install if it does not have in Ubuntu: `sudo apt install snapd`

After installation, use it by: `snap search <application>` `sudo snap install <application>`

### Install ROOT via SNAP
`sudo snap install root-framework`


### Analysis
* in terminal
  
`snap run root-framework` or `root`

`root pet.root` open a root file

`.ls` show info

`branch name->GetEntries()` number of events

`branch name->Show(eventid)` info of an event

`.q` exit

`TBrowser b` open a interactive browser
#### Check hits info
todo
#### Check singles info
todo
#### Check coincidences info
todo

* in Python
  
 `pyroot` (instead of `python`) `>>> import ROOT`

`pyroot root.py`

### Install uproot to read and write root files
🌟🌟🌟another way (Python) to read and write root file:    
`pip install uproot` [Tutorial](https://uproot.readthedocs.io/en/latest/basic.html)
#### Check hits info
```
todo

```
#### Check singles info
```
todo

```
#### Check Coincidence info
```
todo

```
