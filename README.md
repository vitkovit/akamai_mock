# Akamai Multi Tool

## Search
* Search for customer account 
Error will pop up if there is no security configuration available
Copy "account ID" together with "Contract Type Id" which basically forms "Switch Key"
Each new search will refresh tab.
each time account is selected it will generate new view in Configurations and Policies tabs

## Cofigurations
List all configurations for selected account.
List Policies will list policies for selected configuration.
Analyze RC helps visualize Rate Control tuning.
    - it goes through each configuration version and extract policy ID
    - create graph with x-axis that shows version numbers, y-axis show thresholds number
    - creates graph for each unique policy ID, display name of policy from last configuration version
Tab will be refreshed if new customer account is selected.

## Policies
Displays all policies after List Policies is selected.
List hostnames will display all hostnames in Hostnames tab.

## Hostnames
Display all hostnames from selected Security Policy
Provides option to Select/Unselect All
Selected hostname will show up in WAF Test tab in drop down menu.
Check Live will send ping reqeust to each selected hostname by sending 3 ping reqeusts (use multithread to complete task faster)
Check Edge will use nslookup tool to check if hostname is on Akamai platform by searching keyword "akamai" in CNAME 
it checks hostname by adding edgekey and edgesuite suffixes to nslookup
Set staging - TBD

## Host table 
internal tool that will help manage local host table.
Modify local host table by adding ip and hostname pair (x.x.x.x example.com)
by clicking on Modify Hosts File it will ask for password to keep sudo session and modify table with inserted values
by clicking on Reverse Changes, it will delete all changes done by script at any time.
Display Hosts File will read current status of local host table.
nslookup tool is built in tool to help resolve hostnames on the spot. 

## WAF Test 
Send basic attack traffic to selected hostnames.
One hostname at the time can be selected.
Toggle between HTTP and HTTPS 
When ready Send Test will send Attack simulated traffic to hostname
Open WSA will open WSA link with multi dimension filter and public IP in main filter.
Suggestion is to use VPN when testing traffic.

## RC Tester 
Test Rate Control for entered hostname.
enter just host in first field and select HTTP or HTTPS protocol.
Path is optional, if not entered it will use root path.
Number of Requests will send up to 100 requests at once, it will open n number of threads.
Number of Seconds will send n number of requests each second.
Possible to select other HTTP Methods
Send will count down number of seconds.
    - backend tool will need to finish the job first, then it will start countdown

## Updates 
Script has local file named version.py where you can see current version of script.
When new version is available on Git it will compare local version with remote version
Download will open browser and allow to download script from git in zip format.
View Ready is what is done now.

## Latest added Feature:
- copy button for each switch key
- error popup if there is no available security configuration
- Host table now support simple nslookup tool to avoid use of native console
- listing hostname will check all hostname with policy option: Hostnames
ALL Hostnames

## prerequisites 
Must have active API credentials. To create API credentials, go:
Control Center -> search for "Akamai Technologies - Assets" account ->
navigate to Identity & access -> Create API client.

Once you have proper credentials, make sure you have .edgerc file

File location on MAC: ~/.edgerc

edit file with API credentials:
--- Example of .edgerc file ----
[default]
client_secret = xxxxxxxxxxxxxxxxxxx
host = akab-xxxxxxxxxxxxxxxxxxx
access_token = akab-xxxxxxxxxxxxxxxxxxx
client_token = akab-xxxxxxxxxxxxxxxxxxx

if you use different API Section, make sure you change content of version.py file
- modify variable __apisection__ to the name of your API Section

more info can be found on tehcdocs:
https://techdocs.akamai.com/developer/docs/set-up-authentication-credentials

## How to Install and Run script - MAC users 
option 1:
Open install.command with terminal (Terminal should be default selection)
          if not: 
          click on file -> Open With -> Other… -> Applications -> Utilities (scroll to the bottom of screen) -> Enable: All Applications -> Terminal

- it will install brew and python3.11 if is not present
- it will add execute flag to run.sh and Akamai Multitool.command
- it will create virtual environment in local folder, activate and download necessary libraries
- script will always run in virtual environment until is deleted
- after installation application can be start by double click on run.sh
- to remove script simply delete the whole folder 

Option 2:
open terminal
run command:  
> make install
- it will install all dependencies and create virtual environment
> make run
- it will run the script

## How to Install and Run script - Windows users 
TBD

## Upcoming fixes and features 

- automatically adding staging to host table
- option to comment out existing host entries
- search hostnames in API match target
- listing exceptions from WAF rules 
- .edgerc file can now be reeded from windows and mac 
- use of local certificate to check internal git raw files

