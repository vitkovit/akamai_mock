# GUI_propery_creator


########## Search ##########

Search for customer account 
Error will pop up if there is no security configuration evailable
Copy "account ID" together with "Contract Type Id" which basicaly forms "Switch Key"
Each new search will refresh tab
each time account is selected it will generate new view in Cofigurations and Policies tabs

########## Cofigurations ##########

########## Policies ##########

########## Hostnames ##########

########## Host table ##########

########## WAF Test ##########

########## RC Tester ##########

########## Updates ##########

Latest added Feature:
- copy button for each switch key
- error popup if there is no available security configuration
- Host table now support simple nslookup tool to avoid use of native console
- listing hostname will check all hostname with policy option: Hostnames
ALL Hostnames

########## prerequisites ##########

Must have active API credentials. To create API credentials go:
Control Center -> search for "Akamai Technologies - Assets" account ->
navigate to Identity & access -> Create API client

Once you have proper credentials, make sure you have .edgerc file

File location on MAC: ~/.edgerc

edit file with API credentials:
--- Example of .edgerc file ----
[default]
client_secret = xxxxxxxxxxxxxxxxxxx
host = akab-xxxxxxxxxxxxxxxxxxx
access_token = akab-xxxxxxxxxxxxxxxxxxx
client_token = akab-xxxxxxxxxxxxxxxxxxx

if you use different API Section make sure you chnage content of version.py dile
- modify variable __apisection__ to the name of your API Section

more info can be found on tehcdocs:
https://techdocs.akamai.com/developer/docs/set-up-authentication-credentials

########## How to Install and Run script - MAC users ##########

option 1:
Open install.command with terminal (Terminal should be default selection)
          if not: 
          click on file -> Open With -> Other… -> Applications -> Utilities (scroll to the bottom of screen) -> Enable: All Applications -> Terminal

- it will install brew and python3.11 if is not present
- it will add execute flag to run.sh and Akamai Multitool.command
- it will create virtual environemnt in local folder, activate and download neccessary libraries
- script will always run in virtual environment until is deleted
- after instalation application can be start by double click on run.sh
- to remove script simply delete the whole folder 

Option 2:
open terminal
run command:  
> make install
- it will install all dependencies and create virtual environment
> make run
- it will run the script

########## How to Install and Run script - Windows users ##########

TBD
