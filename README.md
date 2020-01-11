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
- [Intermediate python for data science](resources/datacamp/intermediata_python_for_data_science.pdf)
- [Pandas foundations](resources/datacamp/pandas_foundations.pdf)
- [Writing your own functions](resources/datacamp/python_data_science_toolbox_1.pdf)
- [Statistical plots with seaborn](resources/datacamp/introduction_to_data_visualization_with_python.pdf)
- [Plotting 2D arrays](resources/datacamp/introduction_to_data_visualization_with_python.pdf)
- [Python data science toolbox part 2](resources/datacamp/python_data_science_toolbox_2.pdf)
- [Cleaning data in python](resources/datacamp/cleaning_data_in_python.pdf)
- [Python data science toolbox part 1](resources/datacamp/python_data_science_toolbox_1.pdf)

`* Only a few chapters had to be completed in order to compy with the requirements. As such no proof of completeion is 
awarded. A screenshot of the completed courses is added instead`

## Building a foundation
In order to get more familiar with Python I worked on a small [side project](https://github.com/kiwigod/Flight-Tickets) 
which can later on be used to do simple regression predictions on. The idea is to retrieve as many prices for flights 
from point A to B. Along with the price the airline and number of transfers can also be taken into account.

id | departure time | arrival time | departure IATA | arrival IATA | Airline(s) | Duration (minutes) | Price(EUR) | transfers | timestamp 
--- | --- | --- | --- | --- | --- | --- | --- | --- | ---
27694 | 2020-04-09 10:35:00 | 2020-04-09 07:15:00 | AMS | ICN | Air France | 820 | 760 | 1 | 2019-12-22 13:30:07
27693 | 2020-04-09 08:00:00 | 2020-04-09 07:15:00 | AMS | ICN | KLM, Air France | 975 | 705 | 1 | 2019-12-22 13:30:07
27692 | 2020-04-09 11:55:00 | 2020-04-09 08:20:00 | AMS | ICN | Finnair | 805 | 675 | 1 | 2019-12-22 13:30:07
27691 | 2020-04-09 09:45:00 | 2020-04-09 13:45:00 | AMS | ICN | SWISS, Asiana | 1260 | 568 | 0 | 2019-12-22 13:30:07
27690 | 2020-04-09 14:50:00 | 2020-04-09 11:25:00 | AMS | ICN | Lufthansa | 815 | 478 | 1 | 2019-12-22 13:30:07
27689 | 2020-04-09 14:40:00 | 2020-04-09 12:55:00 | AMS | ICN | Turkish Airlines | 915 | 472 | 1 | 2019-12-22 13:30:07
27688 | 2020-04-09 21:25:00 | 2020-04-09 14:55:00 | AMS | ICN | KLM | 630 | 732 | `null` | 2019-12-22 13:30:07
27687 | 2020-04-09 21:20:00 | 2020-04-09 15:05:00 | AMS | ICN | Korean Air | 645 | 682 | `null` | 2019-12-22 13:30:07
27686 | 2020-04-09 08:55:00 | 2020-04-09 05:40:00 | AMS | ICN | Lufthansa | 825 | 472 | 1 | 2019-12-22 13:30:07
_A few rows from the database the flight info is stored in_

As can be observed there's a zero value for transfers in one of the flights. This is just a parse issue that often 
happens with routes which take a long time to get to their final destination.

I've ran the program for over a month every half hour of my laptop's uptime.I do realize now that the data points are 
quite inconsistent, and the data set could quite likely be improved by running it on a server with more uptime than my 
local machine. However since this was just to build some familiarity with Python I decided to just leave it as is.

I've learned quite a bit about Python by building this, and do see some things which could've been solved or built more 
elegantly with the knowledge I've acquired throughout the minor. In the end I did use the project to find and book a 
relatively cheap flight to South Korea in late March! 

## Data set
The data set we received from the LUMC was in a raw format, in other words sensor data.
This data set was accompanied with several Matlab scripts to convert the sensor data to
euler angles. The result is a csv file containing 

### Labels
 
