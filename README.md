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

Finally, with this comes three other important files. 

	1) A text file to start the programme -> "openQCM_Q-1_Scarlet_Start"
	2) A python code to incorporate all of the sweep data file into one csv file -> "Scarlet_SweepTestIntegrator" in openQCM_Q-1_py_v2.1_Scarlet -> OPENQCM -> logged_data -> "Scarlet_SweepTestIntegrator"
	3) A text file to start (2) -> "Scarlet_SweepTestIntegrator"

1) This must be changed for your computer, an example is given but essentially you must edit the text file slightly for it to work.
 	
	a) In the first line, after 'call' is the location of your anaconda3 'activate.bat' script file. This will most likely be found in C: -> Users -> YourAccountName -> anaconda3 -> Scripts -> activate.bat. After this you should then make sure the directory for your anaconda3 environment is stated, again C: -> Users -> YourAccountName -> anaconda3
	
	b) In the second line, after 'cd' you need the directory of the openQCM Q-1 application, this will be wherever you saved the software. So find where you saved the software and navigate to the folder "OPENQCM". You can then change the example directory to this directory.
	
	c) Leave this line unchanged
	
	d) "pause" just prevents the CMD Prompt from closing down in the event of a failure, allowing for easier troubleshooting. You can remove this line if the software opens without fail.

Now you must convert this text file (.txt) to a batch file (.bat). This is done by "Save as" and then adding ".bat" to the end (without quotation marks). It is difficult to edit this code once you have converted it so making a copy of the text file is recommended.
	
2) This should be left in its folder but upon loading it will ask for the directory of the sweep data, just copy and paste the directory when prompted.

3) This is very similar to (1) and must be changed for your computer, an example is given but essentially you must also edit this text file.
 	
	a) Same as in (1a). In the first line, after 'call' is the location of your anaconda3 'activate.bat' script file. This will most likely be found in C: -> Users -> YourAccountName -> anaconda3 -> Scripts -> activate.bat. After this you should then make sure the directory for your anaconda3 environment is stated, again C: -> Users -> YourAccountName -> anaconda3
	
	b) Similar to (1b). In the second line, after 'cd', you need the directory of the Scarlet_SweepTestIntegrator application. Therefore, you must find wherever you saved the software and navigate through the following folders "openQCM_Q-1_py_v2.1_Scarlet" -> "OPENQCM" -> "logged_data". You can then change the example directory to this directory.
	
	c) Same as in (1c), leave this line unchanged
	
	d) Same as in (1d), "pause" just prevents the CMD Prompt from closing down in the event of a failure, allowing for easier troubleshooting. You can remove this line if the software completed integration without fail.

Likewise with (1) Now you must convert this text file (.txt) to a batch file (.bat). This is done by "Save as" and then adding ".bat" to the end (without quotation marks). It is difficult to edit this code once you have converted it so making a copy of the text file is recommended. 
