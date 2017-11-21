# ansible-eos
These are sample playbooks for Arista EOS using eapi transport and common tasks that are useful to invoke show/config commands.

These playbooks utilize the eos_config and eos_command modules and a provider file for authentication.

---
IMPORTANT NOTE

At the time of this writing, these playbooks will only work if 'enable secret' is disabled on target Arista EOS switches. 

Fix will be available in Ansible 2.4.2 release based on
https://github.com/ansible/ansible/issues/30802

Workaround is to disable 'enable secret' on all target Arista EOS switches or use Ansible devel branch that contains the fix.

Example output you may encounter:

<pre>
[root@localhost ansible]# ansible-playbook arista.yml

PLAY [arista] ******************************************************************

TASK [run show version on remote arista devices] *******************************
fatal: [10.x.x.x]: FAILED! => {"changed": false, "code": 1005, "failed": true, "msg": "CLI command 1 of 2 'enable' failed: <font color=red> permission to run command denied"<font color=red>} to retry, use: --limit @/etc/ansible/arista.retry

PLAY RECAP *********************************************************************
172.16.100.238             : ok=0    changed=0    unreachable=0    failed=1

</pre>


---

Example provider file
<pre>
# /etc/ansible/group_vars/all.yaml
eos_connection:
  host: "{{ inventory_hostname }}"
  username: eapi
  password: letmein
  authorize: yes
  auth_pass: "password"
  transport: eapi
  use_ssl: no
</pre>

Directory structure
<pre>
arista.yml
arista_clean.yml 
hosts
group_vars
└── all.yml
</pre>

Sample hosts file
<pre>
# Arista
[arista]
10.1.1.1
10.1.1.2
etc
</pre>

