```
# Nmap 7.94SVN scan initiated Tue Nov  7 14:07:01 2023 as: nmap -vv --reason -Pn -T4 -sV -p 80 "--script=banner,(http* or ssl*) and not (brute or broadcast or dos or external or http-slowloris* or fuzzer)" -oN /home/kali/pentest/VM/results/10.10.11.219/scans/tcp80/tcp_80_http_nmap.txt -oX /home/kali/pentest/VM/results/10.10.11.219/scans/tcp80/xml/tcp_80_http_nmap.xml 10.10.11.219
Nmap scan report for 10.10.11.219
Host is up, received user-set (0.075s latency).
Scanned at 2023-11-07 14:07:02 EST for 230s

Bug in http-security-headers: no string output.
PORT   STATE SERVICE REASON         VERSION
80/tcp open  http    syn-ack ttl 63 nginx 1.18.0
|_http-chrono: Request times for /; avg: 160.90ms; min: 118.21ms; max: 243.18ms
|_http-wordpress-users: [Error] Wordpress installation was not found. We couldn't find wp-login.php
|_http-comments-displayer: Couldn't find any comments.
|_http-feed: Couldn't find any feeds.
|_http-devframework: Couldn't determine the underlying framework or CMS. Try increasing 'httpspider.maxpagecount' value to spider more pages.
| http-vhosts: 
|_128 names had status 200
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: nginx/1.18.0
|_http-litespeed-sourcecode-download: Request with null byte did not work. This web server might not be vulnerable
|_http-title: Did not follow redirect to http://pilgrimage.htb/
|_http-date: Tue, 07 Nov 2023 19:07:09 GMT; -1s from local time.
| http-headers: 
|   Server: nginx/1.18.0
|   Date: Tue, 07 Nov 2023 19:07:14 GMT
|   Content-Type: text/html
|   Content-Length: 169
|   Connection: close
|   Location: http://pilgrimage.htb/
|   
|_  (Request type: GET)
|_http-mobileversion-checker: No mobile version detected.
|_http-dombased-xss: Couldn't find any DOM based XSS.
| http-useragent-tester: 
|   Status for browser useragent: false
|   Redirected To: http://pilgrimage.htb/
|   Allowed User Agents: 
|     Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)
|     libwww
|     lwp-trivial
|     libcurl-agent/1.0
|     PHP/
|     Python-urllib/2.5
|     GT::WWW
|     Snoopy
|     MFC_Tear_Sample
|     HTTP::Lite
|     PHPCrawl
|     URI::Fetch
|     Zend_Http_Client
|     http client
|     PECL::HTTP
|     Wget/1.13.4 (linux-gnu)
|_    WWW-Mechanize/1.34
|_http-errors: Couldn't find any error pages.
|_http-malware-host: Host appears to be clean
| http-sitemap-generator: 
|   Directory structure:
|   Longest directory structure:
|     Depth: 0
|     Dir: /
|   Total files found (by extension):
|_    
|_http-wordpress-enum: Nothing found amongst the top 100 resources,use --script-args search-limit=<number|all> for deeper analysis)
|_http-fetch: Please enter the complete path of the directory to save data in.
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-jsonp-detection: Couldn't find any JSONP endpoints.
|_http-referer-checker: Couldn't find any cross-domain scripts.
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-drupal-enum: Nothing found amongst the top 100 resources,use --script-args number=<number|all> for deeper analysis)

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Tue Nov  7 14:10:53 2023 -- 1 IP address (1 host up) scanned in 231.19 seconds
```

nginx  1.18.0 - nothing useful

directory listing
```
200      GET      178l      395w     5292c http://pilgrimage.htb/assets/js/custom.js
200      GET      171l      403w     6166c http://pilgrimage.htb/login.php
200      GET     2349l     5229w    50334c http://pilgrimage.htb/assets/css/templatemo-woox-travel.css
200      GET        2l     1283w    86927c http://pilgrimage.htb/vendor/jquery/jquery.min.js
200      GET        7l      942w    60110c http://pilgrimage.htb/vendor/bootstrap/js/bootstrap.min.js
200      GET      186l      505w     4928c http://pilgrimage.htb/assets/css/owl.css
200      GET        5l       27w     1031c http://pilgrimage.htb/assets/js/popup.js
200      GET      171l      403w     6173c http://pilgrimage.htb/register.php
200      GET       94l      234w     3576c http://pilgrimage.htb/assets/css/custom.css
200      GET     6805l    11709w   123176c http://pilgrimage.htb/assets/css/fontawesome.css
200      GET       11l      552w    57997c http://pilgrimage.htb/assets/css/animate.css
200      GET        7l     2223w   194705c http://pilgrimage.htb/vendor/bootstrap/css/bootstrap.min.css
200      GET    16582l    60225w   485937c http://pilgrimage.htb/assets/js/tabs.js
200      GET       15l     1928w   119998c http://pilgrimage.htb/assets/js/isotope.min.js
200      GET      198l      494w     7621c http://pilgrimage.htb/
200      GET        5l       13w       92c http://pilgrimage.htb/.git/config
200      GET        1l        2w       23c http://pilgrimage.htb/.git/HEAD
200      GET       16l       58w     5158c http://pilgrimage.htb/.git/index
200      GET      198l      494w     7621c http://pilgrimage.htb/index.php
```


/.git - use git-dumper (https://github.com/arthaud/git-dumper) to dump content
```
git-dumper  http://pilgrimage.htb/ git 
```


![[Pasted image 20231107220021.png]]

db from dashboard.php
![[Pasted image 20231107220500.png]]

magick version 7.1.0-49 (vuln) - CVE-2022-44268
![[Pasted image 20231107220644.png]]

 