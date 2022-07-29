# ansible_collection

This is a pile of semi-funcitonal Ansible playbooks that I use in day-to-day life.  Here's a breakdown by directory:

/elasticsearch/ - This is for upgrading and maintaining existing elasticsearch nodes with basic configurations.
/external/ and /internal/ - These are jobs to rotate certs and add new sites to any basic NGINX proxy
/filebeat/ - This is for upgrading and maintaining existing filebeat client installs.
/metricbeat/ - This is for upgrading and maintaining existing filebeat client installs.
/kibana/ - This is for upgrading and maintaining existing filebeat client installs.

You should be able to load these as jobs into any Jenkins server w/o too many problems.  I used the following Frestyle job config for these jobs from my Git repo, build it locally, and then execute the ansible scripts:

"Project is Parameterized"- I used just "$HOSTNAME"
"Source Code Management" - Gets my github URL for the repo w/ my credentials.  You'll have to figure that out on your own.
    "Branches to Build" this uses your setting too my friends.
"Invoke Ansible Playbook"
    "Ansible Installation" - This will normally be just "ansible" but whatever symlink or env var you used for your anisble install will work
      "Playbook path" - <target_tool>/<script_name>.yml
      "Inventory" - I set this to "File or Host list" and put in "$HOSTNAME," here.  DON'T FORGET THAT COMMA AT THE END! Jenkins & ansible both need that.
      "Credentials" - Whatever your ansible username/password is.  Should be available from the dropdown menu if you setup your Jenkins users correctly.


