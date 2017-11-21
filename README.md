# ansible-eos
These are sample playbooks for Arista EOS using eapi transport and common tasks that are useful to invoke show/config commands.

These playbooks utilize the eos_config and eos_command modules and provider file for authentication.

Example provider used for these playbooks are:

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

