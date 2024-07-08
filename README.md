# Penetration-Testing-Checklist
A Penetration Testing Checklist for web ensures comprehensive security by systematically identifying and addressing potential vulnerabilities. It covers key areas like authentication, session management, input validation, access controls, and data encryption, enhancing overall web application security.


1.Information Gathering <br>

a)https://dorks.faisalahmed.me/# <br>
b)https://taksec.github.io/google-dorks-bug-bounty/ <br>
c)https://mr-koanti.github.io/shodan <br>
d)https://www.lopseg.com.br/osint <br>
e)https://web.archive.org/web/*/shippit.com* <br>

**Review Webserver Metafiles for Information Leakage** <br>

a)Visit robots.txt in the targeted website. <br>
b)Visit sitemap.xml in the targeted website. <br>

2.Configuration and Deployment Management Testing <br>

Subdomain Enumeration <br>

a)subfinder -d example.com -o subdomains.txt -all -vv <br>
b)cat subdomains.txt | httpx-toolkit > live_subdomains.txt <br>
c)https://subdomainfinder.c99.nl/ <br>

Vulnerability Scanning using Nuclei <br>

a)nuclei -l live_subdomains.txt -o nuclei_reslut.txt <br>
b)nuclei -l live_subdomains.txt -rl 3 -c 2 -o nuclei_reslut.txt <br>
c)subfinder -d target.com -all | httpx | nuclei -t ~/nuclei-templates <br>
d)https://blog.projectdiscovery.io/ultimate-nuclei-guide <br>

Subdomain Takeover <br>

a)subzy run --targets live_subdomains.txt <br>
b)nuclei -l live_subdomains.txt -t ~/nuclei-templates/http/takeovers/ <br>

Port Scan and Service discovery <br>

a)nmap -iL without_https.txt -sV <br>


