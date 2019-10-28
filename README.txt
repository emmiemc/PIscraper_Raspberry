Raspberry PiScraper
Version: 1.0, last updated 2019/10/27
README.txt, last updated 2019/10/27

Developed by Emilie Campbell, M.Sc.
Credit: Robert Campbell, M.S.



#-----
#-----
#-----



#-----WHAT IT IS:
PiScraper is a webscraper that checks for updates to prescribing information (PI) on manufacturer websites. When updated, a PDF of the new PI is either downloaded or created, and  put into a folder. The outdated copy is moved to an archival folder for continued access

PiScraper does not have access to red-line labels or any other labels that have not received FDA approval or have not yet been published online

Raspberry PiScraper is specifically written for use on the Raspberry Pi, however it should work with most Linux machines. For the Unix/Mac package, please see the Apple PiScraper package here: https://github.com/emmiemc/PiScraper_Apple



#-----UPDATES:
The most recent versions of PiScraper are hosted at: https://github.com/emmiemc/PiScraper_Apple and https://github.com/emmiemc/PiScraper_Raspberry 

v1.0:
Launch of Raspberry PiScraper, for Raspbian Buster



#-----
#-----
#-----



#-----SYSTEM REQUIREMENTS:
	Raspbian Buster/Debian 10
	poppler-utils: https://poppler.freedesktop.org/
	
	OPTIONAL, used for notification e-mails:
	msmtp: https://marlam.de/msmtp/
	msmtp-mta
	mailutils: https://mailutils.org

Download the necessary packages by entering the language below into your command line:

	sudo apt-get install poppler-utils msmtp msmtp-mta mailutils



#-----FILES:
The installation package for this should include a zipped folder with:

* README.txt
* LICENSE.txt
* /_CODE
	* PiScraper.cmd

PDFs of PIs will be housed in the /PiScraper folder

Once you've run PiScraper at least once, two more folders: /_ARCHIVED (in /PiScraper) and /_LOGS (in /_CODE) will appear. Outdated PIs which have been replaced by new versions will be housed in the ARCHIVED folder, and run logs will be housed in the LOGS folder



#-----INSTALLATION:
If you are missing any of the system requirements listed above, please see the associated installation instructions on how to download them before running PiScraper

If you would like to set up PiScraper to run automatically via the crontab, please see the crontab installation instructions at the bottom of the file to add PiScraper to your crontab



#-----
#-----
#-----



#-----NOTIFICATIONS:
The following instructions are how to send e-mail notifications from an @gmail address. They are not exclusive to gmail, and can be adapted to other domains however. These instructions have been adapted from WashU's ESE 205 documentation, see here: https://classes.engineering.wustl.edu/ese205/core/index.php?title=SSHing_into_your_Raspberry_Pi_(Buster)

1. On your webbrowser, log in to the desired gmail account. Navigate to: https://myaccount.google.com/lesssecureapps, and set to ‘ON’

2. Open command line

3. Type: sudo apt-get install msmtp msmtp-mta

4. Hit enter

5. Type: nano /etc/msmtprc

6. Hit enter

7. Copy & paste into window, replacing google account information:

	#Generics
	 defaults
	 auth     on
	 tls      on
 
	 tls_trust_file /etc/ssl/certs/ca-certificates.crt

	# log location
	 logfile     ~/.msmtp.log
 
	#gmail
	 account     gmail
	 host        smtp.gmail.com
	 port        587
 
	 from        root@raspi-buster
	 user        <accountname>@gmail.com
	 password    <password>
 
	 account default : gmail

8. Hit control+x

9. Hit y

10. Hit enter

11. Exit command line



#-----
#-----
#-----



#-----AUTO-RUNNING:
See below for instructions on how to add PiScraper to the crontab,a file that lists commands scheduled to run at regular intervals. This will require your computer to be on and have internet access at that time. For more information on how to edit the crontab, or change the auto-run time, please see: https://crontab.guru



Installation instructions:

1. Open command line

2. Type: export VISUAL=nano; crontab -e

3. Hit enter

4. Enter: 0 12 * * 1-5 ~path/PiScraper/_CODE/PiScraper.cmd 2>&1 | tee ~path/PiScraper/_CODE/_LOGS/LOG_`date +\%Y-\%m-\%d`.txt

NOTE: replace "~path" with the filepath to PiScraper file.
Ex: Desktop/PiScraper/_CODE/PiScraper.cmd

NOTE: this will run every weekday at noon and export all output (StdERR and StdOUT) to a log file. Please see https://crontab.guru for more information

5. Hit control+x

6. Hit y

7. Hit enter

5. Exit command line



Uninstallation instructions:

1. Open command line

2. Type: export VISUAL=nano; crontab -e

3. Hit enter

4. Remove PiScraper line

5. Hit control+x

6. Hit y

7. Hit enter

5. Exit command line
