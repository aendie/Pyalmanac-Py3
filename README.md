# Pyalmanac-Py3

**Description**

Pyalmanac is a Python 3 script that creates the daily pages of the Nautical Almanac using the UTC timescale,
which is the basis for the worldwide system of civil time. Official Nautical Almanacs employ a UT timescale (equivalent to UT1).

The 'daily pages' are tables that are needed for celestial navigation with a sextant.
Although you are strongly advised to purchase the official Nautical Almanac, this program will reproduce the tables with no warranty or guarantee of accuracy.

Pyalmanac was developed based on the original *Pyalmanac* by Enno Rodegerdts. Various improvements, enhancements and bugfixes have been added since.

**Current state of Pyalmanac**

Pyalmanac is a somewhat dated program.
Pyalmanac is implemented using the [Ephem](https://rhodesmill.org/pyephem/) astronomical library (originally named PyEphem), which is in 'maintenance mode', however recent improvements have made it acceptable for navigational purposes again.
Ephem relies on XEphem, which was 'end of life' as no further updates to XEphem were planned.
Elwood Charles Downey, the author of XEphem, generously gave permission for their use in (Py)Ephem.

Pyalmanac contains its own star database, now updated with data from the Hipparcos Star Catalogue. 
The GHA/Dec star data now matches a sample page from a Nautical Almanac typically to within 0°0.1'.
As of now, (Py)Ephem will continue to receive critical bugfixes and be ported to each new version of Python.
Pyalmanac still has the advantage of speed over other implementations.

One minor limitation of Ephem is related to the projected speed of Earth's rotation, or "sidereal time", which is more accurate in Skyfield-based almanacs.
Accurate assessment of "sidereal time" minimizes GHA discrepancies in general. (This applies to all celestial objects.)

Given the choice, [SFalmanac](https://pypi.org/project/sfalmanac/) is an up-to-date program with almost identical functionality to Pyalmanac, and it uses [Skyfield](https://rhodesmill.org/skyfield/), a modern astronomical library based on the highly accurate algorithms employed in the [NASA JPL HORIZONS System](https://ssd.jpl.nasa.gov/horizons/).

**NOTE: the Python Package Index (PyPI) edition is here:** https://pypi.org/project/pyalmanac/  
**Users are encouraged to install the PyPI edition instead.**  
NOTE: Pyalmanac contains its own star database - it does not use the version supplied with Ephem. Star names are chosen to comply with official Nautical Almanacs.  

This fork of the original code, which can be found at https://github.com/rodegerdts/Pyalmanac, in general includes:

* **various bugfixes** (in accordance with USNO data), e.g. ...  
     - a declination of 20°60.0 now prints as 21°00.0;  
     - the same applies to times ('03:60' now prints as '04:00');  
     - incorrect date display in the **SHA and Mer.pass** section;  
     - some incorrect/missing dates for sunrise/sunset or moonrise/moonset;  
     - a few incorrect dates for Moon (upper) Transit or Antitransit (lower);  
     - incorrect times (by 1 minute) for Moon (upper) Transit or Antitransit (lower) due to truncation instead of rounding (506 such cases in 2019);  
     - a Mer. Pass. of '6:15:' now prints correctly as '06:15';  
     - an event occuring within 30 seconds before midnight now lists as 00:00 the next day.

* **enhanced functionality**, e.g. ...  
     - more accurate star database (based on the Hipparcos Catalogue);  
     - user input checks are performed when entering the requested data;  
     - a brief version of the tables can be created instead of the whole year;  
     - a '**modern**' table format in addition to the 'traditional' format layout;  
     - **three Moonrise/Moonset** events per day can be shown (e.g. on 7th July 2019 at 70°N);  
     - temporary files are deleted after running 'increments.py'.

* **cosmetic improvements**, e.g. ...  
     - Declinations/Latitudes are N/S instead of positive and negative;  
     - Declinations are always printed with two digits for degrees;  
     - line spacing (row padding) within the tables has been improved;  
     - minor table header improvements;  
     - addition of the minutes symbol on the Moon’s v, d and HP data rows.

* **a few typo corrections**

and the results have been crosschecked with USNO data to some extent.  
(Constructive feedback is always appreciated.)

**UPDATE: Aug 2019**

This includes a minor bugfix, improved and standardised output formatting, and cosmetic enhancements to the code. The idea is to have the same output formatting for both the Ephem-based and Skyfield-based versions. If both are opened in a PDF reader, then simply by switching between tabs will highlight the data that has changed. Also one can now generate multiple years of almanacs with a single run. And output messages can be sent to the console or written to a log file if the log file has been opened.

**UPDATE: Nov 2019**

Declination formatting has been changed to the standard used in Nautical Almanacs. In each 6-hour block of declinations, the degrees value is only printed on the first line if it doesn't change. It is printed whenever the degrees value changes. The fourth line has two dots indicating "ditto". This applies to all planet declinations and for the sun's declination, but not to the moon's declination as this is continuously changing.

This also includes some very minor changes and an improved title page for the full almanac with a star chart that indicates the northern navigational stars.

**UPDATE: Jan 2020**

The Nautical Almanac tables now indicate if the sun never sets or never rises; similarly if the moon never sets or never rises. The constant "search_next_rising_sun" in **config.py** determines how the *SunNeverSets* or *SunNeverRises* state is calculated. The code also has cosmetic improvements.  
P.S. The *Overfull \hbox in paragraph...* messages can be ignored - the PDF is correctly generated.

**UPDATE: Feb 2020**

The main focus was on cleaning up the TeX code and eliminating the *Overfull/Underfull hbox/vbox* messages. Other minor improvements were included.

**UPDATE: Mar 2020**

A new parameter in *config.py* enables one to choose between A4 and Letter-sized pages. A [new approach](https://docs.python.org/3/whatsnew/3.0.html#pep-3101-a-new-approach-to-string-formatting) to string formatting has been implemented:
the [old](https://docs.python.org/2/library/stdtypes.html#string-formatting) style Python string formatting syntax has been replaced by the [new](https://docs.python.org/3/library/string.html#format-string-syntax) style string formatting syntax. 

**UPDATE: Jun 2020**

The Equation Of Time is shaded whenever EoT is negative indicating that apparent solar time is slow compared to mean solar time (mean solar time > apparent solar time).

**UPDATE: Feb 2021**

Minor changes are included here to this original (non-PyPI) edition to reflect some of the adaptation that was required (e.g. integrate *increments.py* into *pyalmanac.py* as Option 5) to create a PyPI (Python Package Index) edition making this original (non-PyPI) and the PyPI editions similar. Both editions create identical almanacs and the [PyPI edition](https://pypi.org/project/pyalmanac/) is the preferred choice for users.

**UPDATE: Apr 2021**

A double moonrise or moonset on the same day is now highlighted for better legibility. Event Time tables can now be generated - these are the tables containing data in hours:minutes:seconds, e.g. sunrise, sunset, moonrise, moonset and Meridian Passage.
Accuracy to to the second of time is not required for navigational purposes, but may be used to compare accuracy with other algorithms. Some internal technical enhancements and minor changes to text are also included.

**UPDATE: May 2021**

The indication of objects (Sun or Moon) continuously above or below the horizon has been corrected.

Regarding Moon Data: ".. .." has been added to indicate that the moonrise/moonset event occurs the following day (at the specified latitude). If there is no moonrise/moonset for two or more consecutive days, black boxes indicate "moon below horizon"; white boxes indicate "moon above horizon". This brings it in line with Nautical Almanacs. (Previously they were only displayed when there was no moonrise *and* no moonset on a single day.)

Correction to Sun Data: "Sun continually above/below horizon" now shown if it applies to both Sunrise and Sunset, or *additionally* to both Civil Twilight Start & End; or *additionally* to both Astronomical Twilight Start & End, i.e. as two, four or six events per day and latitude. This brings it in line with Nautical Almanacs.

&emsp;:smiley:&ensp;Pyalmanac is now available on DockerHub [here](https://hub.docker.com/repository/docker/aendie/pyalmanac).&ensp;:smiley:

The DockerHub image contains a Linux-based OS, TeX Live, the application code, and third party Python imports (including the astronomical library). It can be executed "in a container" on Windows 10 Pro, macOS or a Linux-based OS.

**UPDATE: Jul 2021**

The PDF filenames have been revised:

* modna_\<starting date or year\>.pdf: for Nautical Almanacs in modern style
* modst_\<starting date or year\>.pdf: for Sun Tables in modern style
* tradna_\<starting date or year\>.pdf: for Nautical Almanacs in traditional style
* tradst_\<starting date or year\>.pdf: for Sun Tables in traditional style

One command line argument may be appended to the run command:

* -v to invoke verbose mode (send pdfTeX execution steps to the console)
* -log to preserve the log file
* -tex to preserve the tex file

**UPDATE: Nov 2021**

* Enhanced User Interface includes the possibility to generate tables starting at any valid date, or for any month (within -12/+11 months from today).
* Minor cosmetic improvements ('d'-correction in italics; greek 'nu' replaces 'v'-correction; Minutes-symbol added to SD and d)

Increased accuracy due to the following minor improvements:
* Moon phase (percent illumination) is based on midnight (as opposed to midday)
* Star positions are based on midnight (as opposed to midday)
* Moon v and d for hour ‘n’ are based on “hour ‘n+1’ minus hour ‘n’” as opposed to “hour ‘n’ + 30 minutes minus hour ‘n’ – 30 minutes”

The PDF filenames have been revised (again):

* NAmod_\<starting date or month or year\>.pdf: for Nautical Almanacs in modern style
* STmod_\<starting date or month or year\>.pdf: for Sun Tables in modern style
* NAtrad_\<starting date or month or year\>.pdf: for Nautical Almanacs in traditional style
* STtrad_\<starting date or month or year\>.pdf: for Sun Tables in traditional style

## Requirements

&emsp;Most of the computation is done by the free Ephem library.  
&emsp;Typesetting is typically done by MiKTeX or TeX Live.  
&emsp;Here are the requirements/recommendations:

* Python v3.4 or higher (the latest version is recommended)
* Ephem >= 3.7.6 (4.1 is good; 4.1.1, 4.1.2 or 4.1.3 are faulty)
* MiKTeX&ensp;or&ensp;TeX Live

## Files required in the execution folder:

* &ast;.py
* Ra.jpg
* A4chartNorth_P.pdf

### INSTALLATION GUIDELINES on Windows 10:

&emsp;Install Python 3.9.1 (should be in the system environment variable PATH, e.g. )  
&emsp;&ensp;**C:\\Python39\Scripts;C:\\Python39;** .....  
&emsp;Install MiKTeX 21.1 from https://miktex.org/  
&emsp;When MiKTeX first runs it will require installation of additional packages.  
&emsp;Run Command Prompt as Administrator, go to your Python folder and execute, e.g.:

&emsp;**cd C:\\Python39**  
&emsp;**python.exe -m pip install --upgrade pip**  
&emsp;... for a first install:  
&emsp;**pip3 uninstall pyephem ephem**  
&emsp;**pip3 install ephem**  
&emsp;... if already installed, check for upgrade explicitly:  
&emsp;**pip3 install --upgrade ephem**  

&emsp;Put the Pyalmanac files in a new folder, run Command Prompt and start with:  
&emsp;**py -3 pyalmanac.py**

&emsp;If using MiKTeX 21 or higher, executing 'option 5' (Increments and Corrections) will probably fail with  
&emsp;**! TeX capacity exceeded, sorry [main memory size=3000000].**  
&emsp;To resolve this problem (assuming MiKTeX has been installed for all users),  
&emsp;open a Command Prompt as Administrator and enter:  
&emsp;**initexmf --admin --edit-config-file=pdflatex**  
&emsp;This opens **pdflatex.ini** in Notepad. Add the following line:  
&emsp;**extra_mem_top = 1000000**  
&emsp;and save the file. Problem solved. For more details go [here](https://tex.stackexchange.com/questions/438902/how-to-increase-memory-size-for-xelatex-in-miktex/438911#438911)

### INSTALLATION GUIDELINES on Ubuntu 19.10 or 20.04:

&emsp;Ubuntu 18.04 and higher come with Python 3 preinstalled,  
&emsp;however pip may need to be installed:  
&emsp;**sudo apt install python3-pip**

&emsp;Install the following TeX Live package:  
&emsp;**sudo apt install texlive-latex-extra**

&emsp;Install the required astronomical library:  
&emsp;**pip3 uninstall pyephem ephem**  
&emsp;**pip3 install ephem**

&emsp;Put the Pyalmanac files in a folder and start with:  
&emsp;**python3 pyalmanac.py**  


### INSTALLATION GUIDELINES on MAC:

&emsp;Every Mac comes with python preinstalled.  
&emsp;(Please choose this version of Pyalmanac if Python 3.* is installed.)  
&emsp;You need to install the Ephem library to use Pyalmanac.  
&emsp;Type the following commands at the commandline (terminal app):

&emsp;**sudo easy_install pip**  
&emsp;**pip uninstall pyephem ephem**  
&emsp;**pip install ephem**  

&emsp;If this command fails, your Mac asks you if you would like to install the header files.  
&emsp;Do so - you do not need to install the full IDE - and try again.

&emsp;Install TeX/LaTeX from http://www.tug.org/mactex/

&emsp;Now you are almost ready. Put the Pyalmanac files in any directory and start with:  
&emsp;**python pyalmanac**  
&emsp;or  
&emsp;**./pyalmanac**
