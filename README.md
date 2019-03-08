# Learning Ansible

## Playbooks
A list of dictionaries! Or, more specifically, a list of _plays_. A playbook should contain:
* A set of _hosts_ to configure
* A list of _tasks_ to be executed on those hosts

Plays also support optional settings, such as:

`name` _A comment that describes what the play is about; Ansible prints this out when the play starts to run._

`become` _If true, Ansible will run every task by becoming (by default) the root user. This is useful when managing Ubuntu servers, since by default you cannot SSH as the root user._

`vars` _A list of variables and values._

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

## Modules
Scripts that come packaged with Ansible to perform some action on a host.

### Example Modules
`apt`
_Installs or removes packages by using the apt package manager._

`copy`
_Copies a file from local machine to the hosts._

`file`
_Sets the attribute of a file, symlink, or directory._

`service`
_Starts, stops, or restarts a service._

`template`
_Generates a file from a template and copies it to the hosts._
