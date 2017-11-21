# ansible-eos
These are sample playbooks for Arista EOS using eapi transport and common tasks that are useful to invoke show/config commands.

These playbooks utilize the <b>eos_config</b> and <b>eos_command</b> modules and a provider file for authentication.

---
IMPORTANT NOTE

Unless you are running Ansible 2.4.2 or a devel branch containing the fix for:

https://github.com/ansible/ansible/issues/30802

these playbooks will NOT work if 'enable secret' is configured on target Arista EOS switches. 

Workarounds are to (1) disable 'enable secret' on all target Arista EOS switches or (2) use Ansible devel branch that contains the fix.

Example output you may encounter:

"permission to run command denied"

<pre>
[root@localhost ansible]# ansible-playbook arista.yml

PLAY [arista] ******************************************************************

TASK [run show version on remote arista devices] *******************************
fatal: [10.1.1.1]: FAILED! => {"changed": false, "code": 1005, "failed": true, "msg": "CLI command 1 of 2 'enable' failed: permission to run command denied" to retry, use: --limit @/etc/ansible/arista.retry

PLAY RECAP *********************************************************************
10.1.1.1             : ok=0    changed=0    unreachable=0    failed=1

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

