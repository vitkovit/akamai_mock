### Fixes & features: 
#### __version__ 0.3.0
- New functionalities under the **Hostnames** tab:<br>
  - The **Check Property Hostname** button will check and display the “Edge Hostname” for the selected “Property Hostname”. <br>It will also display the staging IP and staging “Edge Hostname”, and create a new button called **Set Staging**.<br>
  - The **Set Staging** button will set up the (staging-ip hostname) to the local host table, asking for write credentials in the process.<br>
- The **Set Staging** button has been removed from the Host table tab. <br>The right window will automatically display when the tab is open or when the “Modify Hosts File” or “Reverse Changes” buttons are used.

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

This will:<br>
* Install brew and python3.11 if not present.<br>
* Add execute flag to _run.sh_ and _main.py_.<br>
* Create a virtual environment in local folder, activate it and download necessary libraries.<br>
* The script will always run in virtual environment until 'venv' folder it is deleted.<br>
* After installation, the application can be started by double clicking on _run.sh_.<br>
* To remove the script, simply delete the whole folder.<br>

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
* Script has local file named version.py where you can see current version of script.<br>
* When new version is available on Git it will compare local version with remote version.<br>
* Download will open browser and allow to download script from git in zip format.<br>
* View Ready is what is done now.<br>

## Latest added Feature:
* Copy button for each switch key.<br>
* Error popup if there is no available security configuration.<br>
* Host table now supports simple nslookup tool to avoid use of native console.<br>
* Listing hostname will check all hostname with policy option: Hostnames ALL Hostnames.<br>

## Upcoming fixes and features
* ~~Selecting from which version and what policy when pressing "Analyze RC".~~<br>
* ~~Automatically adding staging to host table.~~<br>
* ~~Search hostnames in API match target.~~<br>
* Listing exceptions from WAF rules.<br>
* Use of local certificate to check internal git raw files.<br>
* ~~check hostname in property, when Hostnames tab tools failed.~~<br>
* add Bot test tool.<br>
* add options for pragma headers.<br>
* Adding quick SiteShield updates check.<br>
* ~~Fixed color when user do not use Dark Mode in OS.~~<br>
* nslookup tools is broken when it listing too many configurations.<br>

### KNOWN BUGS:
- version lookup can't be done from local git repo due to certificate need<br>
- Download can't automaticaly open local download location due to certificate need, instead it will open browser session<br>
- The "Open ACC" command is designed to initiate the opening of two separate tabs in your web browser. Please note that due to certain limitations, direct redirection via the script is not possible.<br>

### Releases explained
The versioning of this tool follows the format ____version____ = "x.y.z", where:<br>
- **x**: This number changes when a new tab is added to the tool or when there are significant changes. This represents major versions.<br>
- **y**: This number increases when the tool is reorganized or a new tool is added to the existing tool. This represents minor versions.<br>
- **z**: This number changes when there are fixes and changes to the source code. This represents patches or bug fixes.<br>

### Changelog
#### __version__ 0.2.1
- View Readme is showing proper HTML format
#### __version__ 0.2.0
- Two new features have been introduced to the Analyze RC:.<br>
  - A selection window will appear if there are more than 50 versions, allowing you to choose the starting version for analysis..<br>
  - If there are more than 5 Rate Control policies, you will be able to select which one to analyze in a new window.<br>
- Hostnames tab now have __Check Property Hostname__ option, it will list productionCnameTo from all hostnames for an account.<br>
- Configurations tab now shows the latest version number.<br>
- Hostnames tab presents a sorted list of hostnames.<br>
#### __version__ 0.1.2
- fixed issue when Rate Control Policy does not have a name in latest version.<br>
- Host table will now automatically Display Hosts File.<br>
- Host table nslookup tool is rearranged for more intuitive use.<br>
#### __version__ 0.1.1
- The "Oper ACC" buttons, located under the Configurations and Policies sections, are designed to open ACC. Upon clicking, the first tab of your web browser will display the homepage, followed by the ACC configuration and Policy pages respectively.<br>
#### __version__ 0.1.0
- _edgerc_ file can now be read from windows and mac.<br>
- Host table - each neW entry is now written between the same tags, if new entry is added it will check existence in current hosts table, commenting existing entry is possible by adding '#' in front of entry value.<br>
- Configurations tab title misspell is fixed.<br>
- _install.command_ file now works even if there is empty spaces in script path<br>
- under Policies tab 'check hostnames’ button now check hostnames in API<br>
- added button shortcut to open ACC at configuration level from Configurations tab<br>
- added button shortcut to open ACC at policy level from Policies tab<br>
- releases explained<br>
