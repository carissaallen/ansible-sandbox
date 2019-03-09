# Learning Ansible

## Playbooks
A list of dictionaries! Or, more specifically, a list of _plays_. A playbook should contain:
* A set of _hosts_ to configure
* A list of _tasks_ to be executed on those hosts

Plays also support optional settings, such as:

`name` _A comment that describes what the play is about; Ansible prints this out when the play starts to run._

`become` _If true, Ansible will run every task by becoming (by default) the root user. This is useful when managing Ubuntu servers, since by default you cannot SSH as the root user._

`vars` _A list of variables and values._

### Playbook: web-notls-playbook.yml
Configures a host to run an Nginx web server. Although a proper website should have Transport Layer Security (TLS) encryption enabled, I am leaving this out for simplicity's sake in my first playbook.
#### Run
`ansible-playbook web-notls-playbook.yml`
#### Output
Any Ansible task that runs has the potential to change the state of the host in some way. Ansible modules will first check to see whether the state of the host needs to be changed before taking any action. If the state of the host matches the arguments of the module, Ansible takes no action on the host and responds with a state of `ok`. If there is a difference between the state of the host and the arguments to the module, Ansible will change the state of the host and return `changed`. 
```
PLAY [Configure webserver with nginx] ***************************************************************

TASK [Gathering Facts] ******************************************************************************
ok: [testserver]

TASK [install nginx] ********************************************************************************
ok: [testserver]

TASK [copy nginx config file] ***********************************************************************
changed: [testserver]

TASK [enable configuration] *************************************************************************
ok: [testserver]

TASK [copy index.html] ******************************************************************************
changed: [testserver]

TASK [restart nginx] ********************************************************************************
changed: [testserver]

PLAY RECAP ******************************************************************************************
testserver                 : ok=6    changed=3    unreachable=0    failed=0
```
Ansible's detection of state change: The `install nginx` task was unchanged, which means that, before I ran the playbook, the _nginx_ package had already been installed on the host. The `enable configuration` task was unchanged, which meant that there was already a configuration file on the server that was identical to the file I was copying over. However, the `copy index.html` task was changed, which means the _index.html_ file had not been previously copied to the host.

#### HTML Rendered
<img src="https://github.com/carissaallen/ansible-sandbox/blob/master/playbooks/images/web-notls-browser-output.jpg" alt="Browser Output" height="250">

### Playbook: web-tls-playbook.yml
Manually generate a TLS self-signed certificate. The following command generates files _nginx.key_ and _nginx.crt_ in the _files_ directory. The certificate has an expiration date of 10 years (3,650 days) from the day you create it. 

```
req -x509 -nodes -days 3650 -newkey rsa:2048 -subj /CN=localhost -keyout files/nginx.key -out files/nginx.crt
```

## Modules
Scripts that come packaged with Ansible to perform some action on a host. To show documentation for a particular module:
`ansible-doc module-name`

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
