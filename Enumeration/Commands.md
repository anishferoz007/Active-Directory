# Enumeration

## Using PowerView

Enumerate domain users:

```
Get-DomainUser
```

List a specific property of all the users:

```
Get-DomainUser | select -ExpandProperty samaccountname
```
