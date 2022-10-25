Assign your domain name to the crt_common_name variable and any extra subdomains you want to include in the certificate to the crt_subject_alt_name variable.

Since the playbook is using Cloudflare DNS to validate the Let’s Encrypt certificate, you will also need to assign your Cloudflare API credentials to the cloudflare_* variables. You can either assign them directly in the playbook or pass them in via environment variables by running the commands below before running the playbook:
<pre>
export CF_EMAIL=<your_cloudflare_email>
export CF_API_TOKEN=<your_cloudflare_api_token>
export CF_ZONE=<your_cloudflare_api_zone>
</pre>

Run the Ansible playbook with the following command:
<pre>
ansible-playbook ssl.yml
</pre>