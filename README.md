# Learning Ansible

## Playbooks
### First Playbook 
Configures a host to run an Nginx web server. Although a proper website should have Transport Layer Security (TLS) encryption enabled, I am leaving this out for simplicity's sake in my first playbook.
#### Run
`ansible-playbook web-notls-playbook.yml`
#### Output
```
 _______________________________________
< PLAY [Configure webserver with nginx] >
 ---------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

 ________________________
< TASK [Gathering Facts] >
 ------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [testserver]
 ______________________
< TASK [install nginx] >
 ----------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [testserver]
 _______________________________
< TASK [copy nginx config file] >
 -------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [testserver]
 _____________________________
< TASK [enable configuration] >
 -----------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [testserver]
 ________________________
< TASK [copy index.html] >
 ------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [testserver]
 ______________________
< TASK [restart nginx] >
 ----------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

changed: [testserver]
 ____________
< PLAY RECAP >
 ------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

testserver                 : ok=6    changed=1    unreachable=0    failed=0
```
#### HTML Rendered
<img src="https://github.com/carissaallen/ansible-sandbox/blob/master/playbooks/images/web-notls-browser-output.jpg" alt="Browser Output" height="250">
