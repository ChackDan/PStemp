---
external help file: Microsoft.Azure.Commands.ServiceFabric.dll-Help.xml
online version: 
schema: 2.0.0
---

# Remove-AzureRmServiceFabricNodes

## SYNOPSIS
Remove nodes from the specific node type from a cluster.

## SYNTAX

```
Remove-AzureRmServiceFabricNodes [-ResourceGroupName] <String> [-Name] <String> -NodeType <String>
 -Number <Int32> [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION
Use **Remove-AzureRmServiceFabricNodes** to remove nodes from specific node type from a cluster. The removal proceeds only if it meets clsuter health metrics. 

## EXAMPLES

### Example 1
```
PS c:> Remove-AzureRmServiceFabricNodes -ResourceGroupName myResourceGroup -ClusterName myCluster -NumberOfNodesToRemove 2	-NodeTypeName n1
```

This command will remove 2 nodes from the node type n1, if it is safe to do so.

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

### -NodeType
Node type name

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

### -Number
Number of nodes to remove

```yaml
Type: Int32
Parameter Sets: (All)
Aliases: NumberOfNodesToRemove

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
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### System.Int32
System.String

## OUTPUTS

### System.Object

## NOTES

## RELATED LINKS

