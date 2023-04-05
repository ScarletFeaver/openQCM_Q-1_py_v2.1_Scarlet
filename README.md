# openQCM_Q-1_py_v2.1_Scarlet
My personal modification and fix for the openQCM Q-1 software from openQCM. This code allows for cheaper 6 MHz crystals to be used (and with small modifications 5 MHz and 10 MHz crystals). This code also allows for the correct data to be outputted. 

There are three important points to note

	1) Pre-requesites
	2) PeakFrequencies.txt
	3) Supplementary Code
	
1) There are a few pre-requsite packages necessary to download before you start - I have included the userguide provided by openQCM - "openQCM_Q-1-user_manual". 

The section "Installation Guide" is a good place to look. 
Firstly we must install an anaconda3-5.3.0 environment in python3.7, follow this guide for a good explanation -  https://jamesmccaffrey.wordpress.com/2022/05/10/installing-anaconda3-2020-02-with-python-3-7-6-on-windows-10-11/

Once this is done, there are 2 updates we need to perform (a and b) and 5 packages we need to download (c-g) - a package caled "os" should come with the anaconda3 environment and so there is no need to download this. 

	a) pip
	b) h5yt
	c) pyqtgraph pyserial
	d) progressbar
	e) pandas
	f) natsort
	g) tqdm
		
To download these, open up the CMD Prompt on Windows. Type "cd" and then a space and then copy and paste the directory of your anaconda3 environment, e.g. "C:\Users\YourAccountName\anaconda3" (without the quotation marks). You will only be able to download one at a time so upgrade/download each package individually.
Next, to update (a) you must type specifically (without quotation marks) "pip install --upgrade pip" and hit ENTER on the keyboard. Likewise for (b) instead type "pip install --upgrade h5py" and hit ENTER.


Next, for (c) through to (g) you must type, "conda install packagename" and hit ENTER. Replace "packagename" with the package you wish to download, e.g. "conda install pyqtgraph pyserial" will download (after a short while) the pyqtgraph pyserial package (c).


2) The important aspect for the user is the "PeakFrequencies.txt" file found in openQCM_Q-1_py_v2.1_Scarlet -> OPENQCM -> openQCM -> PeakFrequencies.txt

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

3) Finally, with this comes three other important supplementary files. 

	a) A text file to start the programme -> "openQCM_Q-1_Scarlet_Start"
	b) A python code to incorporate all of the sweep data file into one csv file -> "Scarlet_SweepTestIntegrator" in openQCM_Q-1_py_v2.1_Scarlet -> OPENQCM -> logged_data -> "Scarlet_SweepTestIntegrator"
	c) A text file to start (b) -> "Scarlet_SweepTestIntegrator"

a) This must be changed for your computer, an example is given but essentially you must edit the text file slightly for it to work.
 	
	i) In the first line, after 'call' is the location of your anaconda3 'activate.bat' script file. This will most likely be found in C: -> Users -> YourAccountName -> anaconda3 -> Scripts -> activate.bat. After this you should then make sure the directory for your anaconda3 environment is stated, again C: -> Users -> YourAccountName -> anaconda3
	
	ii) In the second line, after 'cd' you need the directory of the openQCM Q-1 application, this will be wherever you saved the software. So find where you saved the software and navigate to the folder "OPENQCM". You can then change the example directory to this directory.
	
	iii) Leave this line unchanged
	
	iv) "pause" just prevents the CMD Prompt from closing down in the event of a failure, allowing for easier troubleshooting. You can remove this line if the software opens without fail.

Now you must convert this text file (.txt) to a batch file (.bat). This is done by "Save as" and then adding ".bat" to the end (without quotation marks). It is difficult to edit this code once you have converted it so making a copy of the text file is recommended.
	
b) This should be left in its folder but upon loading it will ask for the directory of the sweep data, just copy and paste the directory when prompted.

c) This is very similar to (a) and must be changed for your computer, an example is given but essentially you must also edit this text file.
 	
	a) Same as in (ai). In the first line, after 'call' is the location of your anaconda3 'activate.bat' script file. This will most likely be found in C: -> Users -> YourAccountName -> anaconda3 -> Scripts -> activate.bat. After this you should then make sure the directory for your anaconda3 environment is stated, again C: -> Users -> YourAccountName -> anaconda3
	
	b) Similar to (aii). In the second line, after 'cd', you need the directory of the Scarlet_SweepTestIntegrator application. Therefore, you must find wherever you saved the software and navigate through the following folders "openQCM_Q-1_py_v2.1_Scarlet" -> "OPENQCM" -> "logged_data". You can then change the example directory to this directory.
	
	c) Same as in (aiii), leave this line unchanged
	
	d) Same as in (aiv), "pause" just prevents the CMD Prompt from closing down in the event of a failure, allowing for easier troubleshooting. You can remove this line if the software completed integration without fail.

Likewise with (a) Now you must convert this text file (.txt) to a batch file (.bat). This is done by "Save as" and then adding ".bat" to the end (without quotation marks). It is difficult to edit this code once you have converted it so making a copy of the text file is recommended. 
