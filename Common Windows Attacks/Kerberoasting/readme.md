# Overview

In Active Directory (AD), a Service Principal Name (SPN) is a unique identifier for a service instance. Kerberos uses SPNs to associate a service instance with a service logon account, enabling client authentication without knowing the account name.

When a Kerberos TGS (Ticket Granting Service) ticket is requested, it is encrypted using the service account’s NTLM password hash.

**Kerberoasting** is a post-exploitation attack that exploits this by obtaining a ticket and performing offline password cracking. If the ticket decrypts successfully, the guessed password is the correct service account password.

The effectiveness of this attack depends on the service account's password strength and the encryption algorithm used when generating the ticket. The possible encryption options are:

+ AES (secure)
+ RC4 (weaker, still found in some environments)
+ DES (very outdated and insecure)

# Attack Path

First, we will obtain crackable tickets using Rubeus by leveraging the kerberoast option. This will extract Kerberos TGS tickets for every user with an SPN registered. We will then export the results using the outfile option for further analysis and offline password cracking.

![rubeus command](https://github.com/nsx64/azure-cloud-security-solutions-projects/blob/main/Common%20Windows%20Attacks/Kerberoasting/Images/rubeus-command.png)
![rubeus command](https://github.com/nsx64/azure-cloud-security-solutions-projects/blob/main/Common%20Windows%20Attacks/Kerberoasting/Images/rubeus-result.png)

We have identified three Kerberoastable users, including the Administrator, which is particularly interesting.

Next, we will move the extracted tickets offline for cracking using Hashcat.

For demonstration purposes, we will use John the Ripper (JtR) to crack the password quickly, as it is intentionally simple.

![password crack](https://github.com/nsx64/azure-cloud-security-solutions-projects/blob/main/Common%20Windows%20Attacks/Kerberoasting/Images/password-crack.png)

The password for the svc-iam user is "mariposa" in this case.

With this credential, we can now log into the account and proceed with further actions, such as privilege escalation or lateral movement within the environment.

# Detection

Windows event codes can help correlate these attacks. Event ID 4769 is triggered when a TGS is requested but also logs all service connection attempts, making it noisy for detection. If only AES tickets are used, 4769 becomes a strong indicator. However, detecting RC4 tickets (a non-default setting) should raise an alert for further investigation.

![event viewer](https://github.com/nsx64/azure-cloud-security-solutions-projects/blob/main/Common%20Windows%20Attacks/Kerberoasting/Images/eventviewer-codes-kerberoasting.png)

Despite the high volume of Event ID 4769, we can still detect anomalies by targeting default tool behaviors. For example, using 'Rubeus' extracts tickets for all users with an SPN, allowing us to alert if more than ten tickets are generated within a minute (or fewer, depending on thresholds). Event ID 4769 should be grouped by the requesting user and the originating machine. Ideally, two separate alert rules should be created—one for each. In our test environment, running Rubeus against the SPN users triggered the following AD events:

![event viewer](https://github.com/nsx64/azure-cloud-security-solutions-projects/blob/main/Common%20Windows%20Attacks/Kerberoasting/Images/eventviewer-codes-kerberoasting-requests.png)

![event viewer](https://github.com/nsx64/azure-cloud-security-solutions-projects/blob/main/Common%20Windows%20Attacks/Kerberoasting/Images/eventviewer-codes-kerberoasting-machine.png)

# Prevention:

The success of this attack relies on the strength of the service account’s password. To mitigate risk, limit accounts with SPNs, disable unused ones, and enforce strong passwords—ideally 100+ random characters (max 127 in AD) to make cracking infeasible.

Group Managed Service Accounts (GMSA) offer a secure alternative, as AD automatically manages and rotates their 127-character passwords. They are restricted to specific servers and cannot be used elsewhere. However, not all applications support GMSA, mainly Microsoft services like IIS and SQL. Wherever possible, enforce GMSA for new services and phase out traditional accounts.

Regularly audit and remove SPNs assigned to unused services to minimize exposure.
