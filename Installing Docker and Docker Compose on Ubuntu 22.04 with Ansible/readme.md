Run the docker.yml playbook with the following command:

<pre>ansible-playbook -i inventory docker.yml -u ubuntu -K </pre>

Note: change the user with the one you use to login to your Ubuntu servers.

You should see Ansible run through each of the steps in the playbook on each of the servers defined in the hosts.yml inventory file.
