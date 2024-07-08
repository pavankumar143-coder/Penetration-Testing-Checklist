# Penetration-Testing-Checklist
A Penetration Testing Checklist for web ensures comprehensive security by systematically identifying and addressing potential vulnerabilities. It covers key areas like authentication, session management, input validation, access controls, and data encryption, enhancing overall web application security.


1.Information Gathering <br>

https://dorks.faisalahmed.me/# <br>
https://taksec.github.io/google-dorks-bug-bounty/ <br>
https://mr-koanti.github.io/shodan <br>
https://www.lopseg.com.br/osint <br>
https://web.archive.org/web/*/shippit.com* <br>

**Review Webserver Metafiles for Information Leakage** <br>

Visit robots.txt in the targeted website. <br>
Visit sitemap.xml in the targeted website. <br>

2.Configuration and Deployment Management Testing <br>

Subdomain Enumeration <br>

subfinder -d example.com -o subdomains.txt -all -vv <br>
cat subdomains.txt | httpx-toolkit > live_subdomains.txt <br>
https://subdomainfinder.c99.nl/ <br>

Vulnerability Scanning using Nuclei <br>

nuclei -l live_subdomains.txt -o nuclei_reslut.txt <br>
nuclei -l live_subdomains.txt -rl 3 -c 2 -o nuclei_reslut.txt <br>
subfinder -d target.com -all | httpx | nuclei -t ~/nuclei-templates <br>
https://blog.projectdiscovery.io/ultimate-nuclei-guide <br>

Subdomain Takeover <br>

subzy run --targets live_subdomains.txt <br>
nuclei -l live_subdomains.txt -t ~/nuclei-templates/http/takeovers/ <br>


