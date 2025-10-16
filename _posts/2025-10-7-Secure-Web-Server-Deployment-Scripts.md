# Secure Web Server Deployment Scripts:

## The Idea
To build a set of instructions that easily allows for the secure deployment of an Apache or Nginx server. This was created for my Collegiate Cyber Defense Competition (CCDC) team. 

## Steps Taken
### Step 1 - Initial Research 
I needed to figure out what a secure web server looked like. To do this, 2 main resources. \
Apache
- [Apache Official Documentation](https://httpd.apache.org/docs/2.4/misc/security_tips.html) 
- [Dream Host](https://help.dreamhost.com/hc/en-us/articles/226327268-The-most-important-steps-to-take-to-make-an-Apache-server-more-secure)

Nginx
- [Nginx Official Documentation](https://nginx.org/en/docs/http/configuring_https_servers.html)
- [Dream Host](https://help.dreamhost.com/hc/en-us/articles/222784068-The-most-important-steps-to-take-to-make-an-nginx-server-more-secure)

The basic rules to follow are:
- Keep software up to date
- Do not run as a privileged user
- Hide version & server signatures
- Disable or restrict .htaccess / similar override files (Apache)
- Restrict access by IP / path-level rules
- Protect against DoS/slow attacks (e.g., Slowloris)
- Enforce strong TLS / SSL
- Use a Web Application Firewall (WAF)
- Harden the host environment
- Least privilege everywhere
- Regular monitoring, alerts, and log analysis
- Remove unused modules and minimize features

### Step 2 - Implementation of a secure configuration
The next step was to implement as many of these rules as possible using the web server configurations.
- Keep software up to date
- Ensured the System was up to date with: sudo apt update && sudo apt upgrade
- Turned server Tokens off in the configuration file, hiding the version in the header
- Restricted file access by setting a home directory with <Directory "/var/www/html"> and restriction access with Require all granted, Options FollowSymLinks, and AllowOverride None.
- Can easily add an IP restriction with (Require IP X.X.X.X OR 192.168.0.0/24)
- Added a self-signed certificate and forced HTTPS connections only (Only use this if you are not hosting on a public network. Instead, you can use Let's Encrypt to get a free SSL certificate.

### Step 4 Implementation of a Web Application Firewall (WAF)
#### What is a WAF?
A WAF is a security tool that monitors, filters, and blocks HTTP and HTTPS traffic between a web application and the internet. It acts as a protective layer against common web-based attacks such as SQL injection, cross-site scripting (XSS), and distributed denial-of-service (DDoS) attacks. By inspecting and validating incoming requests, a WAF helps ensure that only legitimate traffic reaches the application.

#### The Implementation:
For this project, I implemented ModSecurity, an open-source WAF known for its flexibility and ease of integration. The setup involved downloading the ModSecurity module and integrating it into the Apache Docker container. Once configured, ModSecurity analyzed incoming web traffic in real time, applying customizable security rules to detect and block malicious requests. This significantly strengthened the web server’s defense against application-layer attacks while maintaining normal user access.

### Step 4 - Implementation of a Fail2ban
#### What is Fail2Ban? 
Fail2Ban is an intrusion prevention system (IPS) that protects servers from brute-force attacks and other unauthorized access attempts. It works by monitoring log files for repeated failed login attempts or suspicious activity that violates predefined rules. When a violation is detected, Fail2Ban automatically updates firewall rules to temporarily or permanently block the offending IP address, reducing the risk of further attacks.

#### The Implementation: 
Integrating Fail2Ban was straightforward thanks to its official Docker image. The setup involved mounting the relevant log directories—such as Apache access logs and system logs—into the container and providing a custom configuration file defining which services and patterns to monitor. Once deployed, Fail2Ban actively analyzed incoming logs and dynamically banned malicious IPs at the network level, enhancing the overall security posture of the server with minimal resource overhead.

### Step 5 - Implementation of a Graylog
#### What is Graylog?
Graylog is a free and open-source log management platform that enables centralized collection, indexing, and analysis of logs from multiple sources. It provides a powerful interface for searching, visualizing, and correlating log data, making it easier to monitor system activity, detect anomalies, and troubleshoot issues across an environment.

#### The Implementation:
Integrating Graylog was more complex compared to the other security tools. Beyond simply transferring log files, the data needed to be properly formatted so Graylog could parse and display it in a human-readable form. To achieve this, I configured Fluent Bit as a log forwarder to process and convert logs into the GELF (Graylog Extended Log Format) before sending them via Syslog to the Graylog server. This setup allowed for real-time log ingestion, structured data analysis, and improved visibility into security events across the environment.

### Step 6 - Using Docker and Docker Compose
The final step was to create a streamlined process for deploying a secure web server. I used Docker to build the initial web server with its secure configurations preconfigured, ensuring consistent and repeatable setups. Then, using Docker Compose, I combined the web server with all integrated security tools, allowing them to run together seamlessly. After the initial setup and downloading the required files, the entire secure environment can now be launched with just a few lines of code.






