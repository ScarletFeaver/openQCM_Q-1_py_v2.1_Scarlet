# openQCM_Q-1_py_v2.1_Scarlet
My personal modification and fix for the openQCM Q-1 software from openQCM. This code allows for cheaper 6 MHz crystals to be used (and with small modifications 5 MHz and 10 MHz crystals). This code also allows for the correct data to be outputted.

The important aspect for the user is the "PeakFrequencies.txt" file found in openQCM_Q-1_py_v2.1_Scarlet -> OPENQCM -> openQCM -> PeakFrequencies.txt

The file "PeakFrequencies.txt" was meant to update with the peak frequencies found during peak detection of calibration. However, cheaper crystals have less well-defined frequency responses and so peak detection fails, thus PeakFrequencies.txt never changes. This previously led to errors in measurement where the wrong frequency was recorded.

As provided the PeakFrequencies.txt file is 2 identical columns (space delimited) of three numbers. As is, the software is set to run 6 MHz crystals. That is, runnnig the software will automatically select the 6  MHz option. Clicking "Start" will show this in the "info" window, specically "@6MHz" and "fundamental" for the fundamental frequency. 

To measure a 5 MHz crystal the user must go into the PeakFrequencies.txt file and delete the two rows for 6 MHz and 10 MHz frequencies (make sure there is only one row and two columns of ~5.000000000000000000e+06. Restarting the software and clicking "Start" should now update the "info" window to "@5MHz" and "fundamental".

To measure a 10 MHz crystal the user must go into the PeakFrequencies.txt file and add enough rows so that there are 5 rows and two columns. Just add placeholder numbers to make up these rows, ensure the columns are still identical (see below for example). It is better to make the first number the fundamental frequency of the crystal you wish to measure (e.g. 1.000000000000000000e+07). Restarting the software and clicking "Start" should now update the "info" window to "@10MHz" and "fundamental".
              
			Example
              1.000000000000000000e+07 1.000000000000000000e+07
              3.000000000000000000e+06 3.000000000000000000e+06
              5.000000000000000000e+06 5.000000000000000000e+06
              6.000000000000000000e+06 6.000000000000000000e+06
              8.000000000000000000e+06 8.000000000000000000e+06
							

MOST IMPORTANTLY -> Before running anymeasurements, it is important to do a calibration first, once this has completed inspect the survey produced in the top right-hand graph, find the exact frequency of the peak and then adjust the the respective rows of PeakFrequencies.txt file to reflect this and make the subsequent measurements more accurate. This ensures the measurement window captures the best portions of the peak (more of the lower frequency side captured than the upper frequency side to account for frequency decreases during mass loading). For example, if the peak frequency is measured at 5.985 MHz then alter the 6.000000000000000000e+06 6.000000000000000000e+06 row to 5.985000000000000000e+06 5.985000000000000000e+06.

Finally, with this comes three other pieces of code. 
    1) A batch file to start the programme
    2) A python code to incorporate all of the sweep data file into one csv file.
    3) A batch file to start (2).
