Once you have installed Ansible and have setup your Ubuntu server, add the IP address along with the following hostnames to your local hosts file.
<pre>
10.1.1.21     ubuntu
10.1.1.21     helloworld.com
</pre>
Step 1: Create Inventory File

First, we will create a folder to store the Ansible files in.
<pre>
cd
mkdir ansible && cd ansible
</pre>
Create a file called inventory.yml then add the following:
<pre>
web:
  hosts:
    ubuntu
  vars:
    domain: helloworld.com
    ansible_user: ubuntu
    ansible_ssh_private_key_file: ~/.ssh/id_rsa
    ansible_sudo_pass: qwerty
</pre>

Create NGINX Template File

Create a folder called templates:
<pre>
mkdir templates
</pre>
Create a file inside the templates folder called site.conf.j2 and add the following:
<pre>
server {
  listen 80;
  listen [::]:80;
  server_name {{ domain }};
  root /var/www/{{ domain }};
  location / {
    try_files $uri $uri/ =404;
  }
}
</pre>

Create a folder to store the example static website.
<pre>
mkdir site
</pre>
Add a html file called index.html to the folder:
<pre>
<!DOCTYPE html>
<html lang="en">
  <title> </title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="https://unpkg.com/tachyons/css/tachyons.min.css">
  <body>
    <article class="vh-100 dt w-100 bg-dark-pink">
      <div class="dtc v-mid tc white ph3 ph4-l">
        <h1 class="f6 f2-m f-subheadline-l fw6 tc">Hello World!</h1>
      </div>
    </article>
  </body>
</html>
</pre>
Create a playbook called sync.yml and add the following:
<pre>
- hosts: web
  tasks:
  - name: "sync website"
    synchronize:
      src: site/
      dest: /var/www/{{ domain }}
      archive: no
      checksum: yes
      recursive: yes
      delete: yes
    become: no
    </pre>

Run the playbook to install and configure NGINX:
<pre>
ansible-playbook -i inventory.yml nginx.yml
</pre>

Run the playbook to sync the website files:
<pre>
ansible-playbook -i inventory.yml sync.yml
</pre>