### AD-HOC
```
ansible all -i prod.ini -u root -m ping
 
ansible all -i prod.ini -u root -m command -a 'uptime'
#same
ansible all -i prod.ini -u root -a 'uptime' 
 
ansible elastic all -i prod.ini -u root -a 'uptime'
 
ansible all --limit app -i inventory.ini -m ping
```

for local
```
[local]
localhost ansible_connection=local
```


### PLAYBOOK
### ===========
```
ansible-playbook playbook.yml -i inventory.ini
ansible-playbook --check playbook.yml -i inventory.ini -t nginx
#except tags
ansible-playbook --check playbook.yml -i inventory.ini --skip-tags nginx 

#inventory
ansible-inventory -i inventory.ini --list
```

### YML
### ===========
```
- hosts: webservers

  tasks:
    - name: install redis server
      ansible.builtin.apt:
        name: redis-server
        state: present
        update_cache: yes
      become: yes # <---

    - name: remove redis server
      ansible.builtin.apt:
        name: redis-server
        state: absent
      become: yes # <-
```
      
      
### HANDLERS
### ====================
```
- hosts: webservers
  tasks:
    - name: install nginx
      ansible.builtin.apt:
        name: nginx
        state: latest
      become: yes

    - name: update nginx config
      ansible.builtin.copy:
        src: files/nginx.conf
        dest: /etc/nginx/nginx.conf
      notify:
        - restart nginx
      become: yes

  handlers:
    - name: restart nginx
      ansible.builtin.service:
        name: nginx
        state: reloaded
      become: yes
```
