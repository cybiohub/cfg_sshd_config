![alt text][logo]

# Cybionet - Ugly Codes Division

## SUMMARY

Here is a sshd_config configuration file for the SSHD service annotate according to Cybionet standards.


## "FEATURES"

- Complies with STIG recommendations
- Complies with Cisofy recommendations
- Complies with RHEL CCE recommendations
- Verification done with ssh-audit for
	- Key exchange algorithms
	- Host-key algorithms
	- Encryption algorithms
	- Message authentication code algorithms
- And a lot of useful comments in the configuration.
- Uses a restricted group to allow the user to login via SSH.


## RESTRICTED GROUP

1. Create the restricted group.

```bash
sudo groupadd restricted
```

2. Then add your user to this group.

```bash
sudo usermod -a -G restricted yourusername
```

3. Add a sudoers file to allow restricted group to use sudo command.

```bash
vim /etc/sudoers.d/restricted
```

and put this line in the file.

```
# Allow all user in restricted group to sudo for all commands.
%restricted ALL=(ALL) ALL
```

4. TEST!! Don't disconnect your SSH session, and try to establish a new SSH connection to see if everything work fine.


## RECOMMENDATION

Use Google-Authenticator or a SSH Key with the SSH service to improve its security.

---
[logo]: ./md/logo.png "Cybionet"
