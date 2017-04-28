---
external help file: Microsoft.Azure.Commands.ServiceFabric.dll-Help.xml
online version: 
schema: 2.0.0
---

# Update-AzureRmServiceFabricReliability

## SYNOPSIS
Update reliability tier of the primary node type in a cluster.

## SYNTAX

```
Update-AzureRmServiceFabricReliability [-ResourceGroupName] <String> [-Name] <String> -Level <ReliabilityLevel>
 [-AutoAddNodes] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION
Use **Update-AzureRmServiceFabricReliability** to update reliability of the primary node type in a  cluster.

## EXAMPLES

### Example 1
```
PS c:> Add-AzureRmServiceFabricReliability -ResourceGroupName myResourceGroup -ClusterName myCluster -ReliabilityLevel Silver
```

This command changes reliability level of the primary nodetype to silver.

## PARAMETERS

### -AutoAddNodes
Automatic adjust nodes number when changing reliability

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: Auto

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Confirm
Prompts you for confirmation before running the cmdlet.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Level
Reliability tier

```yaml
Type: ReliabilityLevel
Parameter Sets: (All)
Aliases: ReliabilityLevel
Accepted values: None, Bronze, Silver, Gold, Platinum

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Name
Name of the cluster
```yaml
Type: String
Parameter Sets: (All)
Aliases: ClusterName

Required: True
Position: 1
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -ResourceGroupName
Name of the resource group.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -WhatIf
Shows what would happen if the cmdlet runs. The cmdlet is not run.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### Microsoft.Azure.Commands.ServiceFabric.Models.ReliabilityLevel
System.Management.Automation.SwitchParameter
System.String

## OUTPUTS

### Microsoft.Azure.Commands.ServiceFabric.Models.PsCluster

## NOTES

## RELATED LINKS

