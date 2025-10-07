# Secure Web Server Deployment Scripts:

## The Idea
To build out a set of instructions to easily be able to deplot a Apache or Nginx server securly. This was created for my CCDC team. 

## Steps Taken
### Step 1 - Initial reasearch 
I needed to figure out what a secure web server looked like. To do this is Used 2 main resources. 
Apache
- [Apache Offical Documentation](https://httpd.apache.org/docs/2.4/misc/security_tips.html) 
- [Dream Host](https://help.dreamhost.com/hc/en-us/articles/226327268-The-most-important-steps-to-take-to-make-an-Apache-server-more-secure)

Nginx
- [Nginx Ooffical Documentation](https://nginx.org/en/docs/http/configuring_https_servers.html)
- [Dream Host](https://help.dreamhost.com/hc/en-us/articles/222784068-The-most-important-steps-to-take-to-make-an-nginx-server-more-secure)

The basic rules to follow are:
- Keep software up to date
- Do not run as privileged user
- Hide version & server signatures
- Disable or restrict .htaccess / similar override files (Apache)
- Restrict access by IP / path-level rules
- Protect against DoS/slow attacks (e.g. Slowloris)
- Enforce strong TLS / SSL
- Use a Web Application Firewall (WAF)
- Harden the host environment
- Least privilege everywhere
- Regular monitoring, alerts, and log analysis
- Remove unused modules and minimize features

  ### Step 2 - Implentation of secure configation
  The next step was to implemnt as many of these rule as possible using the web server configrations.
  - Keep software up to date
    - Ensure the System is up to date with: sudo apt update && sudo apt upgrade 
