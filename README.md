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
[converting patient group 4](#ADD LINK) which will be discussed later in this portfolio.

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
