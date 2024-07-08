# Penetration-Testing-Checklist
A Penetration Testing Checklist for web ensures comprehensive security by systematically identifying and addressing potential vulnerabilities. It covers key areas like authentication, session management, input validation, access controls, and data encryption, enhancing overall web application security.


1.Information Gathering <br>

&nbsp;&nbsp;&nbsp;a)https://dorks.faisalahmed.me/# <br>
&nbsp;&nbsp;&nbsp;b)https://taksec.github.io/google-dorks-bug-bounty/ <br>
&nbsp;&nbsp;&nbsp;c)https://mr-koanti.github.io/shodan <br>
&nbsp;&nbsp;&nbsp;d)https://www.lopseg.com.br/osint <br>
&nbsp;&nbsp;&nbsp;e)https://web.archive.org/web/*/shippit.com* <br>

**Review Webserver Metafiles for Information Leakage** <br>

&nbsp;&nbsp;&nbsp;a)Visit robots.txt in the targeted website. <br>
&nbsp;&nbsp;&nbsp;b)Visit sitemap.xml in the targeted website. <br>

2.Configuration and Deployment Management Testing <br>

Subdomain Enumeration <br>

&nbsp;&nbsp;&nbsp;a)subfinder -d example.com -o subdomains.txt -all -vv <br>
&nbsp;&nbsp;&nbsp;b)cat subdomains.txt | httpx-toolkit > live_subdomains.txt <br>
&nbsp;&nbsp;&nbsp;c)https://subdomainfinder.c99.nl/ <br>

Vulnerability Scanning using Nuclei <br>

&nbsp;&nbsp;&nbsp;a)nuclei -l live_subdomains.txt -o nuclei_reslut.txt <br>
&nbsp;&nbsp;&nbsp;b)nuclei -l live_subdomains.txt -rl 3 -c 2 -o nuclei_reslut.txt <br>
&nbsp;&nbsp;&nbsp;c)subfinder -d target.com -all | httpx | nuclei -t ~/nuclei-templates <br>
&nbsp;&nbsp;&nbsp;d)https://blog.projectdiscovery.io/ultimate-nuclei-guide <br>

Subdomain Takeover <br>

&nbsp;&nbsp;&nbsp;a)subzy run --targets live_subdomains.txt <br>
&nbsp;&nbsp;&nbsp;b)nuclei -l live_subdomains.txt -t ~/nuclei-templates/http/takeovers/ <br>

Port Scan and Service discovery <br>

&nbsp;&nbsp;&nbsp;a)nmap -iL without_https.txt -sV <br>

Origin ip Disclosure <br>

&nbsp;&nbsp;&nbsp;a)https://www.shodan.io/ <br>
&nbsp;&nbsp;&nbsp;b)https://search.censys.io <br>

Broken Link Hijacking <br>

&nbsp;&nbsp;&nbsp;Manually open all subdomain to find and click external links on the subdomains to verify. <br>
&nbsp;&nbsp;&nbsp;python3 BLH.py https://www.example.com/ <br>
&nbsp;&nbsp;&nbsp;blc -rof --filter-level 3 https://example.com/ <br>

Mail Server Misconfiguration <br>

&nbsp;&nbsp;&nbsp;a)Now Email Spoofing happens due to two main reasons : <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1)SPF record not set for the particular email <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2)Missing of DMARC protocol for the particular email <br>
&nbsp;&nbsp;&nbsp;b)Go to your target company and collect all the possible emails of that company <br>
&nbsp;&nbsp;&nbsp;c)Now check the SPF and DMARC record of all the emails : https://mxtoolbox.com/ <br>
&nbsp;&nbsp;&nbsp;d)Now if you get an email (xyz@company.com), then go for its exploitation <br>
&nbsp;&nbsp;&nbsp;e)Visit https://emkei.cz/ in order to exploit the issue <br>
&nbsp;&nbsp;&nbsp;f)Here you’ll need to fill From-email, To and Subject <br>
&nbsp;&nbsp;&nbsp;g)In From-email add the company’s email and in To add your own email and in Subject <br> &nbsp;&nbsp;&nbsp;you can add anything (like Hacking You, Bounty Time etc.) <br>
&nbsp;&nbsp;&nbsp;h)Check your inbox and you’ll get the email from that company which was sent by you <br>

SIGNUP PAGE VULNERABILITIES <br>

No Rate Limit at Signup Page <br>

&nbsp;&nbsp;&nbsp;1)Enter your details in signup form and submit the form <br>
&nbsp;&nbsp;&nbsp;2)Capture the signup request and send it to intruder <br>
&nbsp;&nbsp;&nbsp;3)add $$ to email parameter <br>
&nbsp;&nbsp;&nbsp;4)In the payload add different email address <br>
&nbsp;&nbsp;&nbsp;5)Fire up intruder and check whether it return 200 ok <br>


Hyper Link Injection Vulnerability <br>

&nbsp;&nbsp;&nbsp;1)Go to https://target.com/ and create account with the first name http://attacker.com/ and last name. <br>
&nbsp;&nbsp;&nbsp;2)Now check your email and you notice there is malicious hyperlinks. <br>
&nbsp;&nbsp;&nbsp;3)Hyperlink Injection in Friend Invitation Emails. <br>
&nbsp;&nbsp;&nbsp;4)A user can change their name to a URL in order to send email invitations containing malicious hyperlinks. <br>

Server Side Template Injection on Name parameter during Sign Up process <br>

&nbsp;&nbsp;&nbsp;1)Navigate to the Singup page. <br>
&nbsp;&nbsp;&nbsp;2)Now, in the First Name field, enter the value {{7*7}} <br>
&nbsp;&nbsp;&nbsp;3)Fill in the rest of the values on the Register page and register your account. <br>
&nbsp;&nbsp;&nbsp;4)We have used the payload {{7*7}} here to verify that it is being evaluated at the backend. <br>
&nbsp;&nbsp;&nbsp;5)Now, wait for the welcome/promotional email to arrive in your Inbox. <br>
&nbsp;&nbsp;&nbsp;6)Notice that the email arrives with the Subject as 49. <br>
&nbsp;&nbsp;&nbsp;7)Try all input fields. <br>




