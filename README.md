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

Reflected XSS on Signup Page and Login page <br>

&nbsp;&nbsp;&nbsp;1)Go to https://example.com/signup <br>
&nbsp;&nbsp;&nbsp;2)Just fill up the signup form and don't submit. <br>
&nbsp;&nbsp;&nbsp;3)Open burp suite captures the submit request. <br>
&nbsp;&nbsp;&nbsp;4)Change the value of email parameter from a valid email address to <img src=xonerror=alert(document.domain)> <br>
&nbsp;&nbsp;&nbsp;5)Forward the request and turn the intercept off. <br>
&nbsp;&nbsp;&nbsp;6)Go to browser check. <br>
&nbsp;&nbsp;&nbsp;7)Payload for Username field : <svg/onload=confirm(1)> <br>
&nbsp;&nbsp;&nbsp;8)Payload for Email field : a7madn1@gmail.com'"><svg/onload=alert(/xss/)>, “><svg/onload=confirm(1)>”@x.y <br>

PASSWORD RESET PAGE VULNERABILITIES <br>

No Rate Limiting on Password Reset functionality <br>

&nbsp;&nbsp;&nbsp;a)Find the reset password page on the web application. <br>
&nbsp;&nbsp;&nbsp;b)Enter the email then click reset password <br>
&nbsp;&nbsp;&nbsp;c)Intercept this request in burp suite.. <br>
&nbsp;&nbsp;&nbsp;d)Send it to the intruder and repeat it 50 times. <br>
&nbsp;&nbsp;&nbsp;e)You will get 200 OK status. <br>

Account takeover by password reset functionality <br>

&nbsp;&nbsp;&nbsp;email= victim@gmail.com&email=attacker@gmil.com <br>
&nbsp;&nbsp;&nbsp;email= victim@gmail.com%20email=attacker@gmil.com <br>
&nbsp;&nbsp;&nbsp;email= victim@gmail.com |email=attacker@gmil.com <br>
&nbsp;&nbsp;&nbsp;email= victim@gmail.com%0d%0acc:attacker@gmil.com <br>
&nbsp;&nbsp;&nbsp;email= victim@gmail.com&code= my password reset token <br>

Denial of service when entering a long password

&nbsp;&nbsp;&nbsp;Go Sign up page and Forgot password page <br>
&nbsp;&nbsp;&nbsp;Fill the form and enter a long string in password <br>
&nbsp;&nbsp;&nbsp;Click on enter and you’ll get 500 Internal Server errors if it is vulnerable. <br>
&nbsp;&nbsp;&nbsp;Reference link - https://hackerone.com/reports/840598, https://hackerone.com/reports/738569 <br>

Password reset token leakage via referrer <br>

&nbsp;&nbsp;&nbsp;Go to the target website and request for password reset. <br>
&nbsp;&nbsp;&nbsp;Now check your email and you will get your password reset link. <br>
&nbsp;&nbsp;&nbsp;Click on any social media link you see in that email and password reset page. <br>
&nbsp;&nbsp;&nbsp;Don't change the password before clicking on any external links like social media links for the same website. <br>
&nbsp;&nbsp;&nbsp;Capture that request in burp suite, You will find a reset token in the referer header. <br>

Reset password link sent over unsecured http protocol <br>

&nbsp;&nbsp;&nbsp;Go to the target website and request a password reset. <br>
&nbsp;&nbsp;&nbsp;Check email, you will get a reset password link. <br>
&nbsp;&nbsp;&nbsp;Copy that link paste in the notepad and observe the protocol. <br>

Password Reset Token Leak via X-Forwarded-Host

&nbsp;&nbsp;&nbsp;Intercept the password reset request in Burp Suite <br>
&nbsp;&nbsp;&nbsp;Add or edit the following headers in Burp Suite : Host: attacker.com, X-Forwarded-Host: attacker.com. <br>
&nbsp;&nbsp;&nbsp;Forward the request with the modified header. <br>
&nbsp;&nbsp;&nbsp;Look for a password reset URL based on the host header like : https://attacker.com/reset-password.php?token=TOKEN. <br>

Password Reset Link not expiring after changing password <br>

&nbsp;&nbsp;&nbsp;First You need to create an account with a Valid Email Address. <br>
&nbsp;&nbsp;&nbsp;After Creating An Account log out from your Account and Navigate to Forgot Password Page. <br>
&nbsp;&nbsp;&nbsp;Request a Password Reset Link for your Account. <br>
&nbsp;&nbsp;&nbsp;Use The Password Reset Link And Change The Password, After Changing the Password Login to Your Account. <br> 
&nbsp;&nbsp;&nbsp;Now Use The Old Password Reset Link To Change The Password Again.<br>
&nbsp;&nbsp;&nbsp;If You Are Able to Change Your Password Again Then This Is a Bug. <br>

Password Reset Link not expiring after changing the email




