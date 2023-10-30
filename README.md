## Prerequisites 
Active API credentials. To create API credentials, go to:<br>
Control Center -> search for "Akamai Technologies - Assets" account -> navigate to Identity & access -> Create API client.

Once you have proper credentials, make sure you have a _edgerc_ file and edit the file with your API credentials.<br>
**Linux** /home/{username}/.edgerc<br>
**macOS** /Users/{username}/.edgerc (~/.edgerc)<br>
**Windows** C:\Users\{username}\.edgerc<br>

_Example of .edgerc file_<br>
[default]<br>
client_secret = xxxxxxxxxxxxxxxxxxx<br>
host = akab-xxxxxxxxxxxxxxxxxxx<br>
access_token = akab-xxxxxxxxxxxxxxxxxxx<br>
client_token = akab-xxxxxxxxxxxxxxxxxxx<br>

If you use a different API Section, make sure you change the content of the _version.py_ file - modify variable ___apisection___ to the name of your API Section.

More info can be found on  [TechDocs](https://techdocs.akamai.com/developer/docs/set-up-authentication-credentials)


## How to Install and Run script - MAC users 
### Option 1:
Open _install.command_ with terminal (Terminal should be default selection). If not:<br>
two finger click on file -> Open With -> Other… -> Applications -> Utilities (scroll to the bottom of screen) -> Enable: All Applications -> Terminal (set as default)

This will:
* Install brew and python3.11 if not present.
* Add execute flag to _run.sh_ and _main.py_.
* Create a virtual environment in local folder, activate it and download necessary libraries.
* The script will always run in virtual environment until 'venv' folder it is deleted.
* After installation, the application can be started by double clicking on _run.sh_.
* To remove the script, simply delete the whole folder.

### Option 2:
Open terminal and run command:<br>
_> make install_<br>
This will install all dependencies and create a virtual environment.<br>
_> make run_<br>
This will run the script.

## How to Install and Run script - Windows users 
TBD 
Make file is not native to Windows

## Tabs Functionalities 
### Search
Search for customer account. An error will pop up if there is no security configuration available.<br>
* Copy "account ID" together with "Contract Type Id" which basically forms "Switch Key".<br>
* Each new search will refresh tab.<br>
* Each time an account is selected it will generate a new view in Configurations and Policies tabs.<br>

### Configurations
Lists all configurations for selected account.<br>
* List Policies will list policies for selected configuration.<br>
* Analyze RC helps visualize Rate Control tuning. It goes through each configuration version and extracts <br> policy ID, creates a graph with x-axis that shows version numbers, y-axis show thresholds number, creates a graph for each unique policy ID, displays name of policy from last configuration version.<br>
* Tab will be refreshed if new customer account is selected.<br>

### Policies
Lists all policies after List Policies is selected.<br>
* List hostnames will display all hostnames in Hostnames tab.<br>

### Hostnames
Lists all hostnames from selected Security Policy.<br>
* Provides option to Select/Unselect All. Selected hostname will show up in WAF Test tab in drop down menu.<br>
* Check Live will send ping request to each selected hostname by sending 3 ping requests (uses multithreading to complete task faster).<br>
* Check Edge will use nslookup tool to check if hostname is on Akamai platform by searching keyword "akamai" in CNAME. It checks hostname by adding edgekey and edgesuite suffixes to nslookup.<br>
* Set staging - TBD<br>

### Host table 
Internal tool that helps manage local host table. Modify local host table by adding IP and hostname pair (x.x.x.x example.com).<br>
* By clicking on Modify Hosts File it will ask for password to keep sudo session and modify table with inserted values.<br>
* By clicking on Reverse Changes, it will delete all changes done by script at any time.<br>
* Display Hosts File will read current status of local host table.<br>
* nslookup tool is built in tool to help resolve hostnames on the spot.<br>

### WAF Test 
Sends basic attack traffic to selected hostnames.<br>
* One hostname at a time can be selected.<br>
* Toggle between HTTP and HTTPS.<br>
* When ready Send Test will send Attack simulated traffic to hostname.<br>
* Open WSA will open WSA link with multi dimension filter and public IP in main filter.<br>
* Suggestion is to use VPN when testing traffic.<br>

### RC Tester 
Test Rate Control for entered hostname.<br>
* Enter just host in first field and select HTTP or HTTPS protocol.<br>
* Path is optional, if not entered it will use root path.<br>
* Number of Requests will send up to 100 requests at once, it will open n number of threads.<br>
* Number of Seconds will send n number of requests each second.<br>
* Possible to select other HTTP Methods Send will count down number of seconds - backend tool will need to finish the job first, then it will start countdown.<br>
* status code will show for set of reqeusts in each second<br>

## Updates 
Script has local file named version.py where you can see current version of script.<br>
When new version is available on Git it will compare local version with remote version.<br>
Download will open browser and allow to download script from git in zip format.<br>
View Ready is what is done now.


## Latest added Feature:
* Copy button for each switch key.<br>
* Error popup if there is no available security configuration.<br>
* Host table now supports simple nslookup tool to avoid use of native console.<br>
* Listing hostname will check all hostname with policy option: Hostnames ALL Hostnames.<br>

## Upcoming fixes and features 
* Automatically adding staging to host table.<br>
* Option to comment out existing host entries.<br>
* Search hostnames in API match target.<br>
* Listing exceptions from WAF rules.<br>
* _edgerc_ file can now be read from windows and mac.<br>
* Use of local certificate to check internal git raw files.<br>
* check hostname in property, when Hostnames tab tools failed.<br>
