# TP 8 : Présentation de Ansible

    sudo adduser user-ansible
    su - user-ansible
    sudo apt install python3-pip
    pip install ansible==2.7.10
    (ansible2.7.10) user-ansible@server:~$ ls ansible2.7.10/bin/ansible* -l

    -rwxrwxr-x 1 user-ansible user-ansible  5869 Oct 19 07:07 ansible2.7.10/bin/ansible
    -rwxrwxr-x 1 user-ansible user-ansible  5869 Oct 19 07:07 ansible2.7.10/bin/ansible-config
    -rwxrwxr-x 1 user-ansible user-ansible 11708 Oct 19 07:07 ansible2.7.10/bin/ansible-connection
    -rwxrwxr-x 1 user-ansible user-ansible  5869 Oct 19 07:07 ansible2.7.10/bin/ansible-console
    -rwxrwxr-x 1 user-ansible user-ansible  5869 Oct 19 07:07 ansible2.7.10/bin/ansible-doc
    -rwxrwxr-x 1 user-ansible user-ansible  5869 Oct 19 07:07 ansible2.7.10/bin/ansible-galaxy
    -rwxrwxr-x 1 user-ansible user-ansible  5869 Oct 19 07:07 ansible2.7.10/bin/ansible-inventory
    -rwxrwxr-x 1 user-ansible user-ansible  5869 Oct 19 07:07 ansible2.7.10/bin/ansible-playbook
    -rwxrwxr-x 1 user-ansible user-ansible  5869 Oct 19 07:07 ansible2.7.10/bin/ansible-pull
    -rwxrwxr-x 1 user-ansible user-ansible  5869 Oct 19 07:07 ansible2.7.10/bin/ansible-vault

    sudo nano /etc/hosts 
    192.168.100.20 http1
    
    (ansible2.7.10) user-ansible@server:~$ ansible -i inventaire.ini -m ping http1 --user lo --ask-pass
    SSH password: 
    http1 | FAILED! => {
        "changed": false,
        "module_stderr": "Shared connection to http1 closed.\r\n",
        "module_stdout": "/bin/sh: 1: /usr/bin/python: not found\r\n",
        "msg": "The module failed to execute correctly, you probably need to set the interpreter.\nSee stdout/stderr for the exact error",
        "rc": 127
    }
