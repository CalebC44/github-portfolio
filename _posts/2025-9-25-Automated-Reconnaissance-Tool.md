# Automated Reconnaissance Tool:

## The Idea
Build a lightweight, modular reconnaissance utility that takes a domain or an IP as input and returns an overview of the basic information. I wanted to demonstrate the following:
- basic API usage (e.g., VirusTotal, Shodan),
- wrapping CLI tools (whois, nslookup/dig) from Python,
- producing clean, readable terminal output,
- turning a script into a usable command-line application.

## Steps Taken
### Step 1 - Running Bash Commands in Python
Started out by figuring out how to run BASH commands in a Python script with os.system.
After successfully implementing BASH commands, the next step was to get user input using the **input** command.
Next we use whois and nslookup to get basic information such as domain ownership and the IP address connected to it.
Lastly, using **grep -e*** to make the output human readable.

Resources Used: 
- Bash scripting in Python: https://www.geeksforgeeks.org/python/how-to-run-bash-script-in-python/

### Step 2 - Integrating VirusTotal API
Attempting to integrate VirusTotal into the Python script ran into an issue where Python was not registering the variables url, headers, accept, and x-apikey. 
The first step I did was confirm the request was installed with **sudo apt install python3-request**. After confirming it was installed, I tried just running with other variables and ran into the same issue.
Turns out Bash was running the program as a shell script, not a Python script. To fix it, I had to add a proper shebang to the top of the file if making it executable: **"#! /bin/python3"**. 
Once fixed and I had my API key, it was easy to call the website and get the information.
The next issue I ran into was the output for VirusTotal was in JSON format; I needed a way to clean it up. Solved by importing the JSON Python library and using its functions to clean up the output

Resources Used: 
- Python Request Library: https://pypi.org/project/requests/
- VirusTotal Docs: https://docs.virustotal.com/reference/domain-info
  
### Step 3 - Integrating Shodan API
Next is adding the Shodan API to see if there are any exposed services or infrastructure. Following their official GitHub page, adding it was easy.
However, I did run into an issue where Shodan will only take an IP address. To solve this, we will turn the script into a command-line program.

Resources Used: 
- Shodan github: https://github.com/achillean/shodan-python

### Step 4 - Command-line Application
The final step is making the Python script into a command-line application.
We start by defining our functions (default, shodan, and main). Next we define the commands that can be run (--default & --shodan) and finally add in helpful hints, along with the start of the program. 

Resources Used: 
- Python Script to command line: https://www.youtube.com/watch?v=zi-FIG3efag

## [Code](https://github.com/CalebC44/Personal-Projects/blob/main/Automated-Reconnaissance-Tool)


