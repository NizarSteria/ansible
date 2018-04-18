Use inventory / environment
Un fichier variable / env
Create a template file ==> file / env for all variable
Secret ==> Vault pour chiffrer le fichier ou une variable string,
the best way is to scret vaiable ==> git 
ansible-vault encrypt_string
Tag: use tag in role: to execute one bloc in role
ansible-playbook -i production site.yml --tags ntp
Handler: restart tomcat at the end of the deploiement

Pipeline
Monitoring as code

Example:
---
# file: roles/common/tasks/main.yml

- name: be sure ntp is installed
  yum:
    name: ntp
    state: installed
  tags: ntp

- name: be sure ntp is configured
  template:
    src: ntp.conf.j2
    dest: /etc/ntp.conf
  notify:
    - restart ntpd
  tags: ntp

- name: be sure ntpd is running and enabled
  service:
    name: ntpd
    state: started
    enabled: yes
  tags: ntp

 
