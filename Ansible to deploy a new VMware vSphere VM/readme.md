Install Ansible and pyVmomi

Python should already be installed on Mac but you might need to install pip by running this command.

<pre>sudo easy_install pip</pre>

Once pip is installed, we can use it to install Ansible with the following command.

<pre>sudo pip install ansible</pre>

We also need to install pyVmomi which is the Python SDK for the VMware vSphere API that allows you to manage ESX, ESXi, and vCenter.

<pre>sudo pip install pyvmomi</pre>

That’s all the dependencies installed, we’re now ready to create our Ansible playbook.
Create Ansible Playbook

Ansible playbooks are YAML configuratiom files that describe what actions to run on a remote host. For this example, we’ll create a simple playbook called deploy-vms.yml that will use the community.vmware.vmware_guest module to deply a VM from template.

Create the file.

<pre>nano deploy-vms.yml</pre>

Run the playbook

<pre>ansible-playbook deploy-vms.yml</pre>