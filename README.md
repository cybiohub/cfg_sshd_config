![alt text][logo]

# Cybionet - Ugly Codes Division

## SUMMARY

Here is a configuration file "sshd_config" for the SSHD service, annotated according to Cybionet standards. The parameter values present in this file are optimized to ensure enhanced security.


## "FEATURES"

- Complies with STIG recommendations
- Complies with NIST recommendations
- Complies with Cisofy recommendations
- Complies with RHEL CCE recommendations
- Verification done with ssh-audit for
	- Key exchange algorithms
	- Host-key algorithms
	- Encryption algorithms
	- Message authentication code algorithms
- And a lots of helpful comments in the configuration.
- Use the "SSHAuthorized" group to allow users to connect into the machine via SSH.
- Use the "DelegatedAdmins" group to grant sudo permissions to delegated administrators of the machine.
- Optional, use the "PrivilegiedUsers" group to grant restricted sudo permissions to priviligied users on the machine.


## Granting the correct permissions

### Identify the owners of the SSH server configuration file (NIST CCE-82901-0 & CCE-82898-8

To correctly set the user and group that owns the /etc/ssh/sshd_config file, run the following command:

```bash
sudo chown root:root /etc/ssh/sshd_config
```

Service configuration files determine the functionality of their respective services. Incorrect configuration can lead to vulnerabilities and security holes. It is therefore essential that these files are assigned to the correct user/group to prevent unauthorized changes.

### Validating SSH configuration file permissions [NIST CCE-82894-7]

To correctly set the permissions of the /etc/ssh/sshd_config file, run the following command:

```bash
sudo chmod 0600 /etc/ssh/sshd_config
```

Service configuration files enable or disable essential features. Incorrect configuration can lead to vulnerabilities and compromise security. It is therefore crucial that these files have the correct permissions to prevent unauthorized changes.


## RESTRICTED GROUP FOR SSH ACCESS

1. Create the "SSHAuthorized" group.

```bash
sudo groupadd SSHAuthorized
```

2. Then add your user to this group.

```bash
sudo usermod -a -G SSHAuthorized yourusername
```

3. TEST! Do not disconnect your SSH session, but try to establish a new SSH connection to check if everything works correctly.


## DELEGATED ADMINS GROUP FOR SUDO ACCESS

It is not recommended to use the SSH access group to grant permissions to the "sudo" command. By doing so, you can precisely select which users are allowed to have this privilege, as well as which commands they will be able to execute. If you don't like using the "sudo" command, skip this section.

In this example, we will use the "DelegatedAdmins" group to grant full rights to the "sudo" command to the delegated administrators of the machine.


1. Create the "DelegatedAdmins" group.

```bash
sudo groupadd DelegatedAdmins
```

2. Then add your user to this group.

```bash
sudo usermod -a -G DelegatedAdmins yourusername
```

3. Add a sudoers file to allow "DelegatedAdmins" group to use sudo command.

```bash
sudo vim /etc/sudoers.d/DelegatedAdmins
```

and put this line in the file.

```
# Allow all user in "DelegatedAdmins" group to sudo for all commands.
%DelegatedAdmins ALL=(ALL) ALL
```


## RECOMMENDATION

Use Google Authenticator or an SSH key with the SSH service to enhance its security.

---
[logo]: ./md/logo.png "Cybionet"
