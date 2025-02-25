# C2 and C3 deploy workflow for dynamic-discover-client and harmony-MSH artifacts

This workflow is used to build the C2 and C3 versions of the Harmony application.

After build, the workflow deploys the following artifacts:

- dynamic-discovery-client-{latestVersion}.jar
- harmony-MSH-{latestVersion}.jar

to /opt/harmony-ap/webapps/ROOT/WEB-INF/lib
on both C2 and C3 servers.

The workflow then restarts the harmony-ap service on both servers.

The workflow is triggered for the internal-test environment by a push to the `harmony-xeratec-internal-c2-and-c3` branch of the `harmony-common` repository.

The workflow is triggered for the security-test environment by a push to the `harmony-xeratec-security-c2-and-c3` branch of the `harmony-common` repository.

Inputs required are:

Branch names for the following repositories:

- harmony-common
- harmony-access-point
- harmony-smp
- dynamic-discovery-client

Assumed:

- C2 and C3 have are fully installed and configured with the harmony-ap service running
- harmony-ap is installed in /opt/harmony-ap
- harmony-ap is running as a systemd service

``` yaml

inputs:
      harmony-common-branch:
        description: 'Branch for harmony-common'
        required: true
        default: 'harmony-xeratec-internal-c2-and-c3'
      harmony-access-point-branch:
        description: 'Branch for harmony-access-point'
        required: true
        default: 'harmony-main-xeratec'  
      harmony-smp-branch:
        description: 'Branch for harmony-smp'
        required: true
        default: 'harmony-main-xeratec'
      dynamic-discovery-client-branch:
        description: 'Branch for dynamic-discovery-client'
        required: true
        default: 'harmony-main-xeratec'

```

Secrets required in the XeratecSoftwareDevelopment/harmony-common "internal" and "security" github environments:

- C2_VM_HOST # public IP of the C2 VM
- C2_VM_USER # user to SSH into the C2 VM
- C2_VM_SSH_KEY # SSH key to access the C2 VM

- C3_VM_HOST # public IP of the C3 VM
- C3_VM_USER # user to SSH into the C3 VM
- C3_VM_SSH_KEY # SSH key to access the C3 VM