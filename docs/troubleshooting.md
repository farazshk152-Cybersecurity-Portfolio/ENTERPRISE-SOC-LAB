# Troubleshooting Log

## Issue 1 – Windows Server VM Became Unresponsive

### Symptoms
The Windows Server 2022 VM froze after attempting to mount the VirtualBox Guest Additions CD image.

### Possible Cause
Guest Additions installation caused the guest operating system to become unresponsive.

### Resolution
The virtual machine was safely powered off through VirtualBox Manager and restarted successfully.

### Lessons Learned
Guest Additions are optional for the deployment phase and can be installed later after the server is fully configured.