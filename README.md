# DataScience
Arjun Sardjoe Missier - 15052907

## Introduction
This portfolio describes my achievements as well as my contributions towards the project 

## Table of contents
- [Datacamp](#datacamp)
- [Getting familiar with Python](#building-a-foundation)
- [Data set](#data-set)
    - [labels](#labels)

## Datacamp
A complete overview of all datacamp proof of accomplishments can be found [here](resources/datacamp). For completion all 
completed assignments will be listed below in order of due date.
- [Introduction to python](resources/datacamp/introduction_to_python.pdf)
- [Introduction and flat files*](resources/datacamp/assignments_overview.png)
- [Customizing plots](resources/datacamp/introduction_to_data_visualization_with_python.pdf)
- [Intermediate python for data science](resources/datacamp/intermediate_python_for_data_science.pdf)
- [Pandas foundations](resources/datacamp/pandas_foundations.pdf)
- [Writing your own functions](resources/datacamp/python_data_science_toolbox_1.pdf)
- [Statistical plots with seaborn](resources/datacamp/introduction_to_data_visualization_with_python.pdf)
- [Plotting 2D arrays](resources/datacamp/introduction_to_data_visualization_with_python.pdf)
- [Python data science toolbox part 2](resources/datacamp/python_data_science_toolbox_2.pdf)
- [Cleaning data in python](resources/datacamp/cleaning_data_in_python.pdf)
- [Python data science toolbox part 1](resources/datacamp/python_data_science_toolbox_1.pdf)
> _* Only a few chapters had to be completed in order to comply with the requirements. As such no proof of 
completion is awarded. A screenshot of the completed courses is added instead_

## Building a foundation
In order to get more familiar with Python I worked on a small [side project](https://github.com/kiwigod/Flight-Tickets) 
which can later on be used to do simple regression predictions on. The idea is to retrieve as many prices for flights 
from point A to B. Along with the price the airline and number of transfers can also be taken into account.

ID | Departure time | Arrival time | Departure IATA | Arrival IATA | Airline(s) | Duration (minutes) | Price (EUR) | Transfers | Timestamp 
--- | --- | --- | :---: | :---: | --- | :---: | :---: | :---: | ---
27694 | 2020-04-09 10:35:00 | 2020-04-09 07:15:00 | AMS | ICN | Air France | 820 | 760 | 1 | 2019-12-22 13:30:07
27693 | 2020-04-09 08:00:00 | 2020-04-09 07:15:00 | AMS | ICN | KLM, Air France | 975 | 705 | 1 | 2019-12-22 13:30:07
27692 | 2020-04-09 11:55:00 | 2020-04-09 08:20:00 | AMS | ICN | Finnair | 805 | 675 | 1 | 2019-12-22 13:30:07
27691 | 2020-04-09 09:45:00 | 2020-04-09 13:45:00 | AMS | ICN | SWISS, Asiana | 1260 | 568 | 0 | 2019-12-22 13:30:07
27690 | 2020-04-09 14:50:00 | 2020-04-09 11:25:00 | AMS | ICN | Lufthansa | 815 | 478 | 1 | 2019-12-22 13:30:07
27689 | 2020-04-09 14:40:00 | 2020-04-09 12:55:00 | AMS | ICN | Turkish Airlines | 915 | 472 | 1 | 2019-12-22 13:30:07
27688 | 2020-04-09 21:25:00 | 2020-04-09 14:55:00 | AMS | ICN | KLM | 630 | 732 | `null` | 2019-12-22 13:30:07
27687 | 2020-04-09 21:20:00 | 2020-04-09 15:05:00 | AMS | ICN | Korean Air | 645 | 682 | `null` | 2019-12-22 13:30:07
27686 | 2020-04-09 08:55:00 | 2020-04-09 05:40:00 | AMS | ICN | Lufthansa | 825 | 472 | 1 | 2019-12-22 13:30:07
> _A few rows from the database the flight info is stored in_

As can be observed there's a zero value for transfers in one of the flights. This is just a parse issue that often 
happens with routes which take a long time to get to their final destination.

I've ran the program for over a month every half hour of my laptop's uptime.I do realize now that the data points are 
quite inconsistent, and the data set could quite likely be improved by running it on a server with more uptime than my 
local machine. However since this was just to build some familiarity with Python I decided to just leave it as is.

I've learned quite a bit about Python by building this, and do see some things which could've been solved or built more 
elegantly with the knowledge I've acquired throughout the minor. In the end I did use the project to find and book a 
relatively cheap flight to South Korea in late March! 

## Data set
After visiting and talking to one of the physicians at the LUMC we left with a new, and better labeled data set. In 
this data set we could say with certainty which exercise a patient was performing. As opposed to the data set used 
by the project group last year. The only downside to the newly received data set is that we'd have to convert the 
data ourselves to euler angles in matlab using the provided scripts.

### Conversion
The majority of the initial data conversion is done by [Eddie Versluis](https://github.com/v3rslu1s). Therefor I won't 
go into detail about it too much. I did however put the majority of the effort into 
[converting patient group 4](#conversion-of-patient-group-4) which will be discussed later in this portfolio.

## Reproducing results
Unlike the other groups we had an already quite promising result created by the group who worked on this project last 
year. Because of that we decided to do our best to factually and reliably reproduce their results before moving forward.
This was done by most members of the group individually to really understand what has been done to come to these 
results. The only difference between the two project groups is us using the labeled data received from the LUMC, in 
opposition to them using the unlabeled data set.

[My attempt](https://github.com/kiwigod/ortho) at this is possibly the fastest what's achieved within the current group. 
The way it's setup generates only one object, exercise, which warehouses all important data. I personally didn't see a 
need to create multiple objects like patient group and patient, since all this data can be retrieved by looping through 
the collection which contains these objects. For a complete overview of the overview of the data retrieval see the 
figures below

![visual](resources/reproduce_results/load_files.png)
>_loading the files into memory_

![uml](resources/reproduce_results/load_files_uml.png)
>_uml diagram of data loading_

After loading all the data into memory we'd have to prepare it to feed it into a machine learning model. Since we were 
reproducing a result to verify it's integrity we went the same route for this as the previous group did. This meant 
picking five data points from the exercise's ndarray for every unique exercise combination, assuming the patient has 
performed all expected exercises. This will result one or more ndarrays with a length of 650 (samples * sample length * 
number of exercises = 5 * 26 * 5 = 650).

Finally the data can be split into a train and test set, and fed to the model. Training of the model took on average 
not longer than a minute. The results were in line with what we'd expect, however not as good as achieved by the 
project group from last year.

In verdict my approach in reproducing the results might have been the fastest, but it wasn't well understood by my 
peers with less computer programming experience. Therefor we decided to use a peer's project as base to build upon. 
His was easier to understand and produced results just as good.

## Contributions
We've tried several ideas and techniques to improve the results of the machine learning model. In this chapter I 
will elaborate further on the contributions I've made towards the project, and how they impacted the final product. 

### Raw data
In our project we made a distinct division between the raw and converted (euler angle) data. The structure of 
our data set is as follows

>`├── Category_1`
>`│   ├── 1`
>`│   │   ├── AB1.csv`
>`│   │   ├── AB1.txt`
>`│   │   ├── AB2.csv`
>`│   │   ├── AB2.txt`
>`│   │   ├── AF1.csv`
>`│   │   ├── AF1.txt`
>`│   │   ├── AF2.csv`
>`│   │   ├── ...`
>`│   ├── ...`
>`├── ...`
>_data set structure_

>`x y y y`
>`- z z z`
>`- z z z`
>`- z z z`
>_formatting of a sensor measurement_

We've stored the raw and converted data in the same place. This is for the sake of simplicity and easy retrieval. We 
still use the raw data for visualizing the patient's movement. My contributions towards the visualizations was quite 
minimal, apart from offering help when someone was stuck. I did save the absolute path to the raw data files in their 
respective 'Exercise' object.

### Data conversion
As stated earlier the data we received from the LUMC was raw sensor data output from the flock of birds sensor. This 
data still had to be converted to euler angels by us for them to be useful in our application. To do this I created a 
virtual machine running Ubuntu 19.10. During installation I opted for the minimal application option. Afterwards I 
installed "Matlab R2019b", created a shared folder for data conversion, which completed the setup for the data 
conversion.

#### Matlab script
The first thing I had to do was understand how the matlab script operated. Since I never worked with matlab it was 
quite challenging. Eventually I figured out that most of the relevant processing is done within a file called 
"dat2m_FV.m". This file calibrates the sensor data against a predefined calibration file. This calibration file 
is dependant on the room in which the system is located.

It seems there are two calibration files, presumably the flock of birds system was moved at some point. However 
we only received one calibration file. This could pose a problem since we don't know when the recordings of our data 
were made. We tried to contact the LUMC about this, but to no avail, they weren't able to clear this up. Thus we had 
to assume that the calibration file we received was the correct one. 

Furthermore when applying the calibration both the sensor data and calibration file must be presented in the same 
measurement unit. Because the calibration file is a static variable the script converts the sensor data from 
millimeters to inches — the measurement unit used in the calibration file. 

At the end of the script there's a flag which is enabled under conditions which aren't clear to me. Either way 
when this flag is enabled dummy data is filled for the sensors which aren't recorded. This sounds pretty strange 
to me, since it introduces variables which cannot be accounted for.

#### Free movement exercises

#### Skipped patients

#### Patient group 4

### Data verification

### Split

### Data manager

#### Processors

### CNN data generation

## Proof of contributions
The proof on contributions in generated using `git log --author='yuqi' --all`. I believe most of my contributions are 
committed from my own machine. Thus back traceable using the command above.

Commit|Datestamp|Refs|Message
---|---|---|---
[0195d5c](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/0195d5c9174ce1a640a631e4fa2f75246a844dcd)|2020-01-08|origin/processor_update, processor_update|small combination processor update; pick exercises to include in combinations from config. Added a test config
[115fcc0](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/115fcc04afaff86a024ed2ae15d3ae76c01c229e)|2019-12-24||remove print
[1c8495f](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/1c8495fef703ee4a8d209c2ce7e3aa58bfb8cc92)|2019-12-24||fixed frame generator
[a96a120](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/a96a120a0345abc1d81de7da0bc81a9d58e7c40f)|2019-12-24||removed pre processors; handled in config manager
[ef801f7](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/ef801f7e0d5cba3747f024b2799118855cc62839)|2019-12-20||fixed colour mapping
[3ae6e7a](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/3ae6e7a12b6f64540a40e80ce2a4fa5410a1cabd)|2019-12-20|origin/category4_update, category4_update|cat4 without dummy data
[4fbe88e](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/4fbe88ef647fb9021d4759b05e0447c5118ae7f9)|2019-12-18||configuration manager
[d183bed](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/d183bed4303c542e00cf902ddc34b9e8abb4690d)|2019-12-18||added functions for different data confs
[dcfeeea](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/dcfeeea9ee7ab8691035f240de562ecf73f4faef)|2019-12-18||train is invert
[feb5855](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/feb5855071e15f34aa00640fafcb3dd9f5fd3f8b)|2019-12-18||Added comments; fixed issue with (velocity) padding
[79b43eb](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/79b43eb2e272f4f291cb657d62ded1c7cc90109f)|2019-12-18||Merge branch 'master2.0' of ssh.dev.azure.com:v3/DataScienceMinor/Data%20Science/Data%20Science into master2.0
[2084bec](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/2084bec6d31cda81bb4fddbac505957a918835a9)|2019-12-18||return numpy array instead of list
[5da99f1](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/5da99f1d0fc4b42c5c908fdabf7e023fcff45847)|2019-12-17|refs/stash|WIP on neuralnetwork: a77f06b Creating an image out of data-set
[3b7f9ff](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/3b7f9ff554f26b0c3ad46b1a618e92bfffb3b0cc)|2019-12-17||index on neuralnetwork: a77f06b Creating an image out of data-set
[f6afeb1](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/f6afeb1c93af188f64d328f8759254d75d1f7ced)|2019-12-17||Merge branch 'master2.0' of ssh.dev.azure.com:v3/DataScienceMinor/Data%20Science/Data%20Science into master2.0
[b48a063](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/b48a063f88f5e27dcace8db70ccdb435ec74965b)|2019-12-17||removed deepcopy
[813aeae](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/813aeae82c1a7b9a011928f65ee300e3306e8fd3)|2019-12-13||patient id update
[b26afc0](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/b26afc0e4a400586d3198a4e6e83361dd46c37b6)|2019-12-13||patient id fix
[a02a134](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/a02a13456a925b7723a011dce374d939c983e599)|2019-12-09|origin/validation_split, validation_split|Merge branch 'master2.0' of ssh.dev.azure.com:v3/DataScienceMinor/Data%20Science/Data%20Science into validation_split
[45bef72](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/45bef728db6215d2d37a3e5bb96c3c31c2d79d81)|2019-12-04|origin/tsne_old, tsne_old|created restructure script
[f99b16d](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/f99b16dba0b376d19af85471532a34c1d9861e9d)|2019-12-04||added data prev group
[ba99e33](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/ba99e330f8b9c29a0b6f6de96cb14751d940734d)|2019-12-04||Added validation split function and conf
[795087f](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/795087f252a9a6f486db9fda9434c0d85519d293)|2019-12-04|origin/cat4_update, cat4_update|updated cat4 with new conversion
[10f1c51](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/10f1c513c7b2cacc30c41c530cb54a5a6f208a73)|2019-12-04|origin/partial_learning_batch, partial_learning_batch|create batches based on conf
[0e84014](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/0e84014a2cfb512da61109fead4b5f73f170e456)|2019-12-03||disabled shuffle_train in conf
[4e71b1f](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/4e71b1f3124e5e585eb91095e378fd296025b3d2)|2019-12-03|origin/shuffle, shuffle|added shuffle conf
[fd454bc](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/fd454bce2f2f8184a7bb219ca417636061cc3996)|2019-11-27||transpose raw matrix
[44ac288](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/44ac288bf625963932aabc5264c0b9907643987f)|2019-11-27|origin/data_manager, data_manager|cleanup
[02b29a4](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/02b29a484219340a37c95f6345d0da3b66b9617b)|2019-11-27||global configuration
[99182eb](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/99182eb11c64330b06031f361c4648f4f445bc19)|2019-11-26||yes
[b1a56c0](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/b1a56c05d77d516b927231b7b2035b27ed105243)|2019-11-25||Accept patient groups as param in datamanager
[b04af5e](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/b04af5e7df2246053d997bff65d0a12836c72f4b)|2019-11-24||Added remove_idle and resample preprocessor
[8478669](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/8478669e5418ecfae3d3073660ea55396d36ed13)|2019-11-21||cat 4 update
[f8545b8](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/f8545b883fcc35dd1adef767bd8fb4cce45cb620)|2019-11-21||Updated main
[4c3cf13](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/4c3cf13a4abddb8c5162bc082db3fa4457d2765b)|2019-11-21||Added init for models
[51e9735](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/51e9735fd79411869c64b001a7725f1074d07b2c)|2019-11-21||renamed config attr @eulerspace
[dc52e64](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/dc52e64e28b8546a70d24844e7fd78808d18d683)|2019-11-21||Created init, fixed processor rule
[cf8faeb](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/cf8faeb9e7c3e0d4b766c51add18eb4c1317787c)|2019-11-21||Generate pipeline
[e6ad3bc](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/e6ad3bc7557d3b6585d60f240e998c5e5e31b6d6)|2019-11-21||pull config from master
[d708edc](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/d708edcc8d57ed9a5aac1565ed0c6722b3d2fd7e)|2019-11-21||Changed extend to append
[2907945](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/2907945d55a10c550b7b483b8864577ade507b7a)|2019-11-20||pull config from master
[b904935](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/b90493508522e5731804c70332ab7265a41ad3f2)|2019-11-20||var name change
[dcf996f](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/dcf996f720bf7f7d59ddf0fe39c48369548f3ecd)|2019-11-20||removed unused processor
[f35358a](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/f35358a5764e13884f8f83d702837a8c1c005f76)|2019-11-20||Added occupied space processor
[51b2581](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/51b2581da4f13ce3a325687b371d54c0d2a65e21)|2019-11-20||defined processor rules
[f602ef8](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/f602ef8f141e03cc8b0ae2a71e3dec249e50655d)|2019-11-20||Added new data finalization function
[7244b5d](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/7244b5d7b2f267c52d4ff5e5723d87904139e645)|2019-11-20||renamed datamanager; Moved split functions to a separate class
[8c4acd6](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/8c4acd68555713ca714806d4de2d12a10fb76eae)|2019-11-20||extend list instead of append; Data ready for model training
[67cc991](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/67cc991ecb14a78f1cd94b54f48343f99c87a623)|2019-11-20||generate train/test split
[ba84f76](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/ba84f76157cb7891bf07e591367a6a9a63d01a19)|2019-11-19||small improvements
[77a3d36](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/77a3d3646a32514f9bb64585392545c7efb96db7)|2019-11-19||create split based on delta
[2801bd0](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/2801bd0465fe3856c5324491215be81b54ba3712)|2019-11-19||clean main
[fa45198](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/fa451980bb776aa66374d501734e95c132c76227)|2019-11-19||Added config to interface; Added processor for data finalization
[0b8a710](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/0b8a710311558ee1e8709927f6b69e2d157d9932)|2019-11-19||removed unused function from patientgroup
[56058e5](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/56058e55eb697f2d2343ea84fe9493f52f7540d3)|2019-11-19||renamed config var
[40b7e2c](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/40b7e2c39176ea1594d9cd5a6b311435ba6b8196)|2019-11-19||Added remove_idle rule
[f2a3fe3](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/f2a3fe3a0d7ca74fc81bee614a682ece9e48e590)|2019-11-19||Added send_through
[fc9ec0b](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/fc9ec0bb8215b153980631711b1cfa0bd2636c9f)|2019-11-19||Created processors
[5f19fd9](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/5f19fd93f87467510a13fd835046fcbd89ba2e5f)|2019-11-19|origin/refactor_ml, refactor_ml|tbh cant remember what i did
[5883b03](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/5883b03c90ca5ebc9a8bafeaae91df9a90bae603)|2019-11-13||Added iterator for patient and patientgroup
[de25f7a](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/de25f7ab1d6e84397c30c1def2bcd45473e61536)|2019-11-13|origin/load_free_movement, load_free_movement|Merge branch 'master2.0' of ssh.dev.azure.com:v3/DataScienceMinor/Data%20Science/Data%20Science into load_free_movement
[5b8bb2f](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/5b8bb2fb1b4940a16e786fae7679256cf3d42062)|2019-11-13||load free movement when load_other in patientgroup
[51dc176](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/51dc176340c4488a29060991ee3ebe0224b14c9e)|2019-11-12||Added free movement .csv
[be77c88](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/be77c88b5f5f5f0903c60709783c10f4545bf611)|2019-11-12||Updated cat 2 and 4
[a1abed8](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/a1abed85c35af84c33361abf33ff223760b0ba39)|2019-11-08||Added raw files
[1cba01b](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/1cba01bdc75b5ae3d506cc54c1ffd5962d2829d7)|2019-11-08|origin/master, origin/HEAD|Added raw files
[a1dbccf](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/a1dbccf6ac5017a570ff8d93f0d15f0a489ba4b1)|2019-11-06||Merge branch 'master2.0' of ssh.dev.azure.com:v3/DataScienceMinor/Data%20Science/Data%20Science into master2.0
[6c5ab95](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/6c5ab95b9af543994bf8ca4f8fdca2d6a12d37b4)|2019-11-06||Added raw files
[d0a8aad](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/d0a8aad9126be96ed5f63f79e60564bd76d7ebb9)|2019-11-05||readability of locating data folder
[52f4ecd](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/52f4ecd9cc2fed70eec31777fb61831c704b686e)|2019-11-05|origin/raw_data_location, raw_data_location|replaced size function with default override; save raw path to exercise
[5fb77c5](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/5fb77c56b4c98f21d967f736bd6a269fdad3e341)|2019-11-05||edge case in main
[840ccf6](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/840ccf6d848e426cff03ebf11a912182cba60fe7)|2019-11-05||Cleanup; removed unused .gitignore entries; example config.py
[1a6dd9a](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/1a6dd9a942298910e590e9faa39bd41dea1bcf2a)|2019-11-05||Updated .gitignore
[f50f471](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/f50f471e9ccb32d7acd6908c0da508f478fc34ae)|2019-10-02|origin/dev_arjun, dev_arjun|use SVC to classify patient cat
[42f2c8f](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/42f2c8f61ee37c07bddd63e510b2959cbfbcddbb)|2019-10-01||Added metadata parser; Added Neigbours classifier
[0194c10](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/0194c1091575615ad3b236f6ebc5cc0a04b4fd3d)|2019-09-30||moved train/predict to interface; added linear regression
[1a052d5](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/1a052d5f1c6318aef66397118a1d40681d0c0da5)|2019-09-30||Removed commented code
[b7f7876](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/b7f78765b7025e27d7c06b5838f6c7ae0c369a6d)|2019-09-18||target specific init param
[86dcfed](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/86dcfedb47a338b6cf43efea5faba1b50d89350c)|2019-09-18||dump and load trained model
[1794f3e](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/1794f3e735c662f80630abeb07f6dfec4f271204)|2019-09-18||Added support vector classification
[b1e559b](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/b1e559b1467b57433ae9f618ba28168f21683e1d)|2019-09-11||Added requirements; update .gitignore
[f36edbf](https://dev.azure.com/DataScienceMinor/Data%20Science/_git/Data%20Science/commit/f36edbfcb43619aa3192efd7582e080cdd738591)|2019-09-11||test

## Presentations
I presented and/or contributed towards the following presentations
- [External 1](https://dehaagsehogeschool-my.sharepoint.com/:p:/g/personal/19132565_student_hhs_nl/ETasmawQUflKlnrCcJ2gQSQBvmOvDZmdIikdY7Z9w2wvhQ?e=HApMbH)
- [Week 11 | 18 November](https://dehaagsehogeschool-my.sharepoint.com/:p:/g/personal/19132565_student_hhs_nl/EWpjZddvGttMgWaJVYdXwGYBeOENDjFWd-1NVSs_gZV22w?e=Qw1ooA)
- [Week 14 | 16 December](https://dehaagsehogeschool-my.sharepoint.com/:p:/g/personal/19132565_student_hhs_nl/EZZGNqrN6ItMmVBhbVP4W6gBKBtVIwCSFHikUJW7w0yXRA?e=Q5ul5M)

Within the project group we also did a presentation to share knowledge. Which can be found [here](https://dehaagsehogeschool-my.sharepoint.com/:b:/g/personal/19132565_student_hhs_nl/ET85TZN-LUZFsLATVPHWFKUBDPsRSdUpyvANrJlsKRnmdw?e=ZzNBwM).
My presentation wasn't really in depth about the project, but more or less a overview of what changes we 
could make in the codebase. The aim was to increase flexibility in the code, and not creating code which 
is tailored towards one specific use case.

## Reflections
I believe a reflection should be confidential and thus not shared on a publicly accessible portfolio. I'll therefor 
add them as an attachment when handing in the portfolio.
