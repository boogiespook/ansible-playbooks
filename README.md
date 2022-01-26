# malware-playbooks
This playbook contains a selection of tasks to test out some malware signatures which are picked up by yara/Red Hat Insights.  
Please not that there are *no* live malware binaries here - just signatures which spoof malware incidents.

## Pre-Reqs
 - The RHEL server must be registered to Red Hat Insights:
```
$ sudo yum -y install insights-client
$ sudo insights-client --register
```

The playbook will enable the EPEL repository to install the yara package.

The playbook will carry out the following actions:
- Ensure EPEL is enabled
- Install yara
- Install wget
- Download finspy script
- Run the finspy script in the background
- Get PID of finspy
- Run the Insights malware check
- Kill the finspy process
- Remove finspy script from /var/tmp

Nice and easy to run, just edit the inventory file and change to the FQDN of the server you which to check. The playbook uses tags so to re-run the check without going throug the pre-flight checks, you can just run:
``  
$ansible-playbook malware-check.yaml --skip-tags pre-flight
``
When finished, you can see the results at: https://console.redhat.com/beta/insights/malware/systems

Hopefully more signature to be added in the future!
