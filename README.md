# ansible-eos
These are sample playbooks for Arista EOS using eapi transport and common tasks that are useful to invoke show/config commands.

These playbooks utilize the eos_config and eos_command modules and a provider file for authentication.

---
IMPORTANT NOTE

At the time of this writing, these playbooks will only work if there is NO enable password configured on target Arista EOS switches. This has been fixed and will be available in the Ansible 2.4 release.
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

