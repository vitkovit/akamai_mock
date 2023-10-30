## Prerequisites 
Active API credentials. To create API credentials, go to:<br>
Control Center -> search for "Akamai Technologies - Assets" account -> navigate to Identity & access -> Create API client.

Once you have proper credentials, make sure you have a ```edgerc``` and edit the file with your API credentials.<br>
**Linux** /home/{username}/.edgerc<br>
**macOS** /Users/{username}/.edgerc (~/.edgerc)<br>
**Windows** C:\Users\{username}\.edgerc<br>

_Example of .edgerc file_<br>
[default]<br>
client_secret = xxxxxxxxxxxxxxxxxxx<br>
host = akab-xxxxxxxxxxxxxxxxxxx<br>
access_token = akab-xxxxxxxxxxxxxxxxxxx<br>
client_token = akab-xxxxxxxxxxxxxxxxxxx<br>

If you use a different API Section, make sure you change the content of the ```version.py``` file - modify variable ```__apisection__``` to the name of your API Section.

More info can be found on  [TechDocs](https://techdocs.akamai.com/developer/docs/set-up-authentication-credentials)


## How to Install and Run script - MAC users 
### Option 1:
Open ```install.command``` with terminal (Terminal should be default selection). If not:<br>
two finger click on file -> Open With -> Other… -> Applications -> Utilities (scroll to the bottom of screen) -> Enable: All Applications -> Terminal (set as default)

This will:
- Install brew and python3.11 if not present.
- Add execute flag to ```run.sh``` and ```main.py```.
- Create a virtual environment in local folder, activate it and download necessary libraries.
- The script will always run in virtual environment until 'venv' folder it is deleted.
- After installation, the application can be started by double clicking on ```run.sh```.
- To remove the script, simply delete the whole folder.

### Option 2:
Open terminal and run command:<br>
```> make install```<br>
This will install all dependencies and create a virtual environment.<br>
```> make run```<br>
This will run the script.

## How to Install and Run script - Windows users 
TBD 
Make file is not native to Windows

## Tabs Functionalities 
### Search
Search for customer account. An error will pop up if there is no security configuration available.
* Copy "account ID" together with "Contract Type Id" which basically forms "Switch Key".
* Each new search will refresh tab.
* Each time an account is selected it will generate a new view in Configurations and Policies tabs.

### Configurations
Lists all configurations for selected account.
* List Policies will list policies for selected configuration.
* Analyze RC helps visualize Rate Control tuning. It goes through each configuration version and extracts policy ID, creates a graph with x-axis that shows version numbers, y-axis show thresholds number, creates a graph for each unique policy ID, displays name of policy from last configuration version.
* Tab will be refreshed if new customer account is selected.

### Policies
Lists all policies after List Policies is selected.
* List hostnames will display all hostnames in Hostnames tab.

### Hostnames
Lists all hostnames from selected Security Policy. 
* Provides option to Select/Unselect All. Selected hostname will show up in WAF Test tab in drop down menu.
* Check Live will send ping request to each selected hostname by sending 3 ping requests (uses multithreading to complete task faster).
* Check Edge will use nslookup tool to check if hostname is on Akamai platform by searching keyword "akamai" in CNAME. It checks hostname by adding edgekey and edgesuite suffixes to nslookup.
* Set staging - TBD

### Host table 
Internal tool that helps manage local host table. Modify local host table by adding IP and hostname pair (x.x.x.x example.com).
* By clicking on Modify Hosts File it will ask for password to keep sudo session and modify table with inserted values.
* By clicking on Reverse Changes, it will delete all changes done by script at any time.
* Display Hosts File will read current status of local host table.
* nslookup tool is built in tool to help resolve hostnames on the spot. 

### WAF Test 
Sends basic attack traffic to selected hostnames. 
* One hostname at a time can be selected. 
* Toggle between HTTP and HTTPS. 
* When ready Send Test will send Attack simulated traffic to hostname.
* Open WSA will open WSA link with multi dimension filter and public IP in main filter. 
* Suggestion is to use VPN when testing traffic.

### RC Tester 
Test Rate Control for entered hostname. 
* Enter just host in first field and select HTTP or HTTPS protocol. 
* Path is optional, if not entered it will use root path. 
* Number of Requests will send up to 100 requests at once, it will open n number of threads.
* Number of Seconds will send n number of requests each second. 
* Possible to select other HTTP Methods Send will count down number of seconds - backend tool will need to finish the job first, then it will start countdown.
* status code will show for set of reqeusts in each second

## Updates 
Script has local file named version.py where you can see current version of script.<br>
When new version is available on Git it will compare local version with remote version.<br>
Download will open browser and allow to download script from git in zip format.<br>
View Ready is what is done now.


## Latest added Feature:
* Copy button for each switch key.
* Error popup if there is no available security configuration.
* Host table now supports simple nslookup tool to avoid use of native console.
* Listing hostname will check all hostname with policy option: Hostnames ALL Hostnames.

## Upcoming fixes and features 
* Automatically adding staging to host table.
* Option to comment out existing host entries.
* Search hostnames in API match target.
* Listing exceptions from WAF rules.
* ```edgerc``` file can now be read from windows and mac.
* Use of local certificate to check internal git raw files.
* check hostname in property, when Hostnames tab tools failed
