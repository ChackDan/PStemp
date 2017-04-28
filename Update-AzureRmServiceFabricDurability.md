---
external help file: Microsoft.Azure.Commands.ServiceFabric.dll-Help.xml
online version: 
schema: 2.0.0
---

# Update-AzureRmServiceFabricDurability

## SYNOPSIS
Update the durability tier and VMSku of a nodetype in a cluster.

## SYNTAX

```
Update-AzureRmServiceFabricDurability [-ResourceGroupName] <String> [-Name] <String> -NodeType <String>
 -Level <DurabilityLevel> [-Sku <String>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION
Use **Update-AzureRmServiceFabricDurability** to update durability and Sku of a NodeType in a cluster.

## EXAMPLES

### Example 1
```
PS c:> Update-AzureRmServiceFabricDurability -ResourceGroupName clusterresourcegroup -ClusterName mycluster -Level Silver -NodeTypeName nt1
```

This command changes durability tier of the node type 'nt1' to silver.

## PARAMETERS

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
DurabilityTier.

```yaml
Type: DurabilityLevel
Parameter Sets: (All)
Aliases: DurabilityLevel
Accepted values: Bronze, Silver, Gold

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Name
Name of the cluster.

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

### -NodeType
Service Fabric node type name.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -ResourceGroupName
Specifies the name of the resource group.

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

### -Sku
Sku of the node type.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -WhatIf
Shows what would happen if the cmdlet runs or not.

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

### Microsoft.Azure.Commands.ServiceFabric.Models.DurabilityLevel
System.String

## OUTPUTS

### Microsoft.Azure.Commands.ServiceFabric.Models.PsCluster

## NOTES

## RELATED LINKS

