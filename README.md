# DevOps HW2 — Ansible Playbook

## Задание

Задание по Ansible:

Написать playbook который должен будет:
- Создать пользователя на удаленной машине.
- Дать пользователю права sudo.
- Сделать авторизацию ssh по ключам для пользователя.
- Отключить авторизацию по паролю при ssh подключении.
- Создать директорию в /opt/ с правами 660 для пользователя.

## Выполнение и результаты:
```
ubuntu@ubuntu:~/devops/martynov-devops-hw2$ ansible-playbook playbook.yml 

PLAY [Configure remote server for DevOps HW2] ****************************************************

TASK [Gathering Facts] ***************************************************************************
ok: [localhost]

TASK [Ensure sudo package is installed] **********************************************************
ok: [localhost]

TASK [Enshure SSH service is enabled and started] ************************************************
ok: [localhost]

TASK [Create user] *******************************************************************************
ok: [localhost]

TASK [Give user sudo rights without password] ****************************************************
ok: [localhost]

TASK [Create .ssh directory for user] ************************************************************
ok: [localhost]

TASK [Add authorized SSH key for user] ***********************************************************
ok: [localhost]

TASK [Disable SSH password authentication] *******************************************************
ok: [localhost]

TASK [Disable SSH keyboard-interactive authentication] *******************************************
ok: [localhost]

TASK [Enable SSH public key authentication] ******************************************************
ok: [localhost]

TASK [Create directory in /opt for user] *********************************************************
ok: [localhost]

PLAY RECAP ***************************************************************************************
localhost                  : ok=11   changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

ubuntu@ubuntu:~/devops/martynov-devops-hw2$ id devopsuser
uid=1002(devopsuser) gid=1003(devopsuser) groups=1003(devopsuser)
ubuntu@ubuntu:~/devops/martynov-devops-hw2$ sudo -l -U devopsuser
Matching Defaults entries for devopsuser on ubuntu:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin,
    use_pty

User devopsuser may run the following commands on ubuntu:
    (ALL : ALL) NOPASSWD: ALL
ubuntu@ubuntu:~/devops/martynov-devops-hw2$ sudo cat /etc/sudoers.d/devopsuser
devopsuser ALL=(ALL:ALL) NOPASSWD:ALL
ubuntu@ubuntu:~/devops/martynov-devops-hw2$ sudo ls -la /home/devopsuser/.ssh
total 4
drwx------ 2 devopsuser devopsuser  60 May 11 20:03 .
drwxr-x--- 3 devopsuser devopsuser 120 May 11 20:03 ..
-rw------- 1 devopsuser devopsuser 748 May 11 20:03 authorized_keys 
ubuntu@ubuntu:~/devops/martynov-devops-hw2$ ssh -o PreferredAuthentications=password -o PubkeyAuthentication=no devopsuser@localhost
devopsuser@localhost: Permission denied.
ubuntu@ubuntu:~/devops/martynov-devops-hw2$ ls -ld /opt/devopsuser_workdir
drw-rw---- 2 devopsuser devopsuser 40 May 11 20:03 /opt/devopsuser_workdir
```
