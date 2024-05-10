# Enumeration

## Using PowerView
### Domain Users

Enumerate domain users:

```
Get-DomainUser
```

List a specific property of all the users:

```
Get-DomainUser | select -ExpandProperty samaccountname
```
### Domain Computers

Enumerate member computers in the domain:

```
Get-DomainComputer | select -ExpandProperty dnshostname
```
### Domain Groups

Enumerate details of the Domain Admins group:

```
Get-DomainGroup -Identity "Domain Admins"
```
### Enterprise Admin Members

Enumerate members of the Enterprise Admins group:

```
Get-DomainGroupMember -Identity "Enterprise Admins"
Get-DomainGroupMember -Identity "Enterprise Admins" -Domain moneycorp.local
```
### OU

list all the OUs:

```
Get-DomainOU
```

See just the names of the OUs:

```
Get-DomainOU | select -ExpandProperty name
```

List all the computers in the X OU:

```
(Get-DomainOU -Identity X).distinguishedname | %{Get-DomainComputer -SearchBase $_} | select name
```

### GPO

List the GPOs:

```
Get-DomainGPO
```

Enumerate GPO applied on the X OU:

```
(Get-DomainOU -Identity X).gplink
```

Copy the highlighted string from above (no square brackets, no semicolon and nothing after semicolon) and use the it below:

```
Get-DomainGPO -Identity '{A-B-C-D}'
```

### ACL

Enumerate ACLs for the Domain Admins Group:

```
Get-DomainObjectAcl -Identity "Domain Admins" -ResolveGUIDs -Verbose
```

Check for modify rights/permissions for the userX, we can use FindInterestingDomainACL from PowerView:

```
Find-InterestingDomainAcl -ResolveGUIDs | ?{$_.IdentityReferenceName -match "userX"}
```

Suppose userX is a member of the RDPUsers group, let us check permissions for it too:

```
Find-InterestingDomainAcl -ResolveGUIDs | ?{$_.IdentityReferenceName -match "RDPUsers"}
```

### Forest

Enumerate all domains in the current forest:

```
Get-ForestDomain -Verbose
```

### Trust

To map all the trusts of the X domain:

```
Get-DomainTrust
```

List only the external trusts in of the X.local forest:

```
Get-ForestDomain | %{Get-DomainTrust -Domain $_.Name} | ?{$_.TrustAttributes -eq "FILTER_SIDS"}
```
