

### The Idea
This tool was developed to be one of my first projects in this portfolio. It is a simple tool that taks in a domain name and cheks among websites such as VirusTotal and Shdoan to see if it is malaicous. 

### idology
How to add more modules or tools. I would create a seperate file and get it working in there before adding it to the main file. 


### The steps taken
Started out by figuring out how to run BASH commands in a python script. After secsfully implenting that the next step was to get user input. 

Once we got user input I found the commands I wanted to use whois and lslookup. Inputing those commands and cleaniing up the out you get basic information about the website.

Running into an issue where python is not regeistering the varabiles url, headers, accept, x-apikey. 
First step was to confirm request was installed with sudo apt install python3-request. 
Turns out bash was not running it as a python script. I had to add "#! /bin/python3" to the top of the file so they stystem knew to run as a python script. 


Next issue the output for VirusTotal is in JSON format so we need a way to clean it up. Solved by imporinting JSON format python library and using its functions to clean up the output

After cleaning up the outputs and putting them together we have our final product! input a domain name and get basic infomation about it.

Next step is adding Shodan to see if there is any exposed services or infrastructure.

###Automated Reconnaissance Tool:

- Goal: Create a Python or PowerShell script that takes a domain name as input and automatically performs basic reconnaissance.

- What it shows: Your ability to use APIs (like VirusTotal or Shodan) and command-line tools (like whois or nslookup) within a script.

- Skills Demonstrated: Python scripting, OSINT (Open-Source Intelligence), API integration.



Resources used:
- Bash scripting in python: https://www.geeksforgeeks.org/python/how-to-run-bash-script-in-python/
- Python Request Library: https://pypi.org/project/requests/
- VirusTotal Docs: https://docs.virustotal.com/reference/domain-info
- Shodan: https://github.com/achillean/shodan-python
- Pyhton Script to command line: https://www.youtube.com/watch?v=zi-FIG3efag

