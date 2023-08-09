---
external help file: Microsoft.Rtc.Management.Hosted.dll-help.xml 
online version: https://learn.microsoft.com/powershell/module/skype/set-cstenantdialplan
applicable: Microsoft Teams
title: Set-CsTenantDialPlan
schema: 2.0.0
manager: bulenteg
author: jenstrier
ms.author: jenstr
ms.reviewer:
---

# Set-CsTenantDialPlan

## SYNOPSIS
Use the `Set-CsTenantDialPlan` cmdlet to modify an existing tenant dial plan.

## SYNTAX

### Identity (Default)
```
Set-CsTenantDialPlan [[-Identity] <string>] [-Description <string>] [-ExternalAccessPrefix <string>]
 [-NormalizationRules <Object>] [-OptimizeDeviceDialing <bool>] [-SimpleName <string>]
 [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION
The `Set-CsTenantDialPlan` cmdlet modifies an existing tenant dial plan. A tenant dial plan determines such things as which normalization rules are applied and whether a prefix
must be dialed for external calls. Tenant dial plans provide required information to let Enterprise Voice users make telephone calls.
The Conferencing Attendant application also uses tenant dial plans for dial-in conferencing.

## EXAMPLES

### -------------------------- Example 1 --------------------------
```
Set-CsTenantDialPlan -ExternalAccessPrefix "123" -Identity vt1tenantDialPlan9
```

This example updates the vt1tenantDialPlan9 tenant dial plan to use an external access prefix of 123.

### -------------------------- Example 2 --------------------------
```
$nr2 = Get-CsVoiceNormalizationRule -Identity "US/US Long Distance"
Set-CsTenantDialPlan -ExternalAccessPrefix "123" -Identity vt1tenantDialPlan9 -NormalizationRules @{Add=$nr2}
```

This example updates the vt1tenantDialPlan9 tenant dial plan to have an external access prefix of 123 and use the US/US Long Distance normalization rules.

### -------------------------- Example 3 --------------------------
```
$DP = Get-CsTenantDialPlan -Identity Global
$NR = $DP.NormalizationRules | Where Name -eq "RedmondFourDigit")
$NR.Name = "RedmondRule"
Set-CsTenantDialPlan -Identity Global -NormalizationRules $DP.NormalizationRules
```

This example changes the name of a normalization rule. Keep in mind that changing the name also changes the name portion of the Identity.
The `Set-CsVoiceNormalizationRule` cmdlet doesn't have a Name parameter, so in order to change the name, we first call the `Get-CsTenantDialPlan` cmdlet to retrieve the Dial Plan with
the Identity Global and assign the returned object to the variable $DP. Then we filter the NormalizationRules Object for the rule RedmondFourDigit and assign the returned object to
the variable $NR. We then assign the string RedmondRule to the Name property of the object. Finally, we pass the variable back to the NormalizationRules parameter of the
`Set-CsTenantDialPlan` cmdlet to make the change permanent.

### -------------------------- Example 4 --------------------------
```
$DP = Get-CsTenantDialPlan -Identity Global
$NR = $DP.NormalizationRules | Where Name -eq "RedmondFourDigit")
$DP.NormalizationRules.Remove($NR)
Set-CsTenantDialPlan -Identity Global -NormalizationRules $DP.NormalizationRules
```

This example removes a normalization rule. We utilize the same functionality as for Example 3 to manipulate the Normalization Rule Object and update it with the 
`Set-CsTenantDialPlan` cmdlet. We first call the `Get-CsTenantDialPlan` cmdlet to retrieve the Dial Plan with the Identity Global and assign the returned object to the variable $DP. 
Then we filter the NormalizationRules Object for the rule RedmondFourDigit and assign it to the variable $NR. Next, we remove this Object with the Remove Method from $DP.NormalizationRules.
Finally, we pass the variable back to the NormalizationRules parameter of the `Set-CsTenantDialPlan` cmdlet to make the change permanent.

## PARAMETERS

### -Confirm
The Confirm switch causes the command to pause processing and requires confirmation to proceed.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: cf
Applicable: Microsoft Teams

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Description
The Description parameter describes the tenant dial plan - what it's for, what type of user it applies to or any other information that helps to identify the purpose of the tenant dial plan.
Maximum characters is 1040.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 
Applicable: Microsoft Teams

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ExternalAccessPrefix
The ExternalAccessPrefix parameter is a number (or set of numbers) that designates the call as external to the organization.
(For example, to tenant-dial an outside line, first dial 9). This prefix is ignored by the normalization rules, although these rules will be applied to the rest of the number.
The OptimizeDeviceDialing parameter must be set to True for this value to take effect.

The value of this parameter must be no longer than 4 characters long and can contain only digits, "#" or a "*".

```yaml
Type: String
Parameter Sets: (All)
Aliases: 
Applicable: Microsoft Teams

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Identity
The Identity parameter is a unique identifier that designates the name of the tenant dial plan to modify.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 
Applicable: Microsoft Teams

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -NormalizationRules
The NormalizationRules parameter is a list of normalization rules that are applied to this dial plan.
Although this list and these rules can be created directly by using this cmdlet, we recommend that you create the normalization rules by the [New-CsVoiceNormalizationRule](https://learn.microsoft.com/powershell/module/skype/New-CsVoiceNormalizationRule) cmdlet, which creates the rule and assigns it to the specified tenant dial plan.

The number of normalization rules cannot exceed 50 per TenantDialPlan.

```yaml
Type: List
Parameter Sets: (All)
Aliases: 
Applicable: Microsoft Teams

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OptimizeDeviceDialing
Use this parameter to determine the effect of ExternalAccessPrefix parameter.
If set to True, the ExternalAccessPrefix parameter takes effect.

```yaml
Type: Boolean
Parameter Sets: (All)
Aliases: 
Applicable: Microsoft Teams

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -SimpleName
The SimpleName parameter is a display name for the tenant dial plan. This name must be unique among all tenant dial plans.

This string can be up to 49 characters long. Valid characters are alphabetic or numeric characters, hyphen (-), dot (.), and parentheses (()).

```yaml
Type: String
Parameter Sets: (All)
Aliases: 
Applicable: Microsoft Teams

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf
The WhatIf parameter describes what would happen if you executed the command, without actually executing the command.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: wi
Applicable: Microsoft Teams

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see about_CommonParameters (https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS

[Grant-CsTenantDialPlan](Grant-CsTenantDialPlan.md)

[New-CsTenantDialPlan](New-CsTenantDialPlan.md)

[Get-CsTenantDialPlan](Get-CsTenantDialPlan.md)

[Remove-CsTenantDialPlan](Remove-CsTenantDialPlan.md)
