---
external help file: Microsoft.Azure.Commands.ServiceFabric.dll-Help.xml
online version: 
schema: 2.0.0
---

# Remove-AzureRmServiceFabricClientCertificate

## SYNOPSIS
Remove a client certificate(s) or certificate subject (s) names from being used for client authenticaton to the cluster

## SYNTAX

### SingleUpdateWithCommonName
```
Remove-AzureRmServiceFabricClientCertificate [-ResourceGroupName] <String> [-Name] <String>
 -CommonName <String> -IssuerThumbprint <String> [-WhatIf] [-Confirm] [<CommonParameters>]
```

### SingleUpdateWithThumbprint
```
Remove-AzureRmServiceFabricClientCertificate [-ResourceGroupName] <String> [-Name] <String>
 -Thumbprint <String> [-WhatIf] [-Confirm] [<CommonParameters>]
```

### MultipleUpdatesWithCommonName
```
Remove-AzureRmServiceFabricClientCertificate [-ResourceGroupName] <String> [-Name] <String>
 -CommonNames <PSClientCertificateCommonName[]> [-WhatIf] [-Confirm] [<CommonParameters>]
```

### MultipleUpdatesWithThumbprint
```
Remove-AzureRmServiceFabricClientCertificate [-ResourceGroupName] <String> [-Name] <String>
 [-AdminClientThumbprints <String[]>] [-ReadonlyClientThumbprints <String[]>] [-WhatIf] [-Confirm]
 [<CommonParameters>]
```

## DESCRIPTION
Use **Remove-AzureRmServiceFabricClientCertificate** to remove a client certificate(s) or certificate subject (s) names from being used for client authenticaton to the cluster

## EXAMPLES

### Example 1
```
PS c:> Remove-AzureRmServiceFabricApplicationCertificate -ResourceGroupName myResourceGroup -ClusterName myCluster -Thumbprint 5F3660C715EBBDA31DB1FFDCF508302348DE8E7A
```

This command removes thumbprint 5F3660C715EBBDA31DB1FFDCF508302348DE8E7A from being used for client authentication to the cluster

### Example 2
```
PS c:> $table = @{"abc.com;AF06E4BFCBA05DCB59C42720136EC19DBA0A8E9F"=$true}
PS c:>Remove-AzureRmServiceFabricClientCertificate -CommonNameIssuersAndFlags $table -ClusterName myclustername -ResourceGroupName myresourcegroup
```

This command removes the certificates with  common name with abc.com and issue thumbprint of 5F3660C715EBBDA31DB1FFDCF508302348DE8E7A from being used for client authentication to the cluster.

## PARAMETERS

### -AdminClientThumbprints
Client certificate thumbprint that have admin privilages to the cluster

```yaml
Type: String[]
Parameter Sets: MultipleUpdatesWithThumbprint
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -CommonName
Client certificate common name.

```yaml
Type: String
Parameter Sets: SingleUpdateWithCommonName
Aliases: 

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -CommonNames
Client common names , issuer thumbprint and authentication type.

```yaml
Type: PSClientCertificateCommonName[]
Parameter Sets: MultipleUpdatesWithCommonName
Aliases: 

Required: True
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

### -IssuerThumbprint
Certificate issuer thumbprint.

```yaml
Type: String
Parameter Sets: SingleUpdateWithCommonName
Aliases: 

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
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -ReadonlyClientThumbprints
Client certificate thumbprint that has read only permissions to the cluster.

```yaml
Type: String[]
Parameter Sets: MultipleUpdatesWithThumbprint
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
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
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Thumbprint
Certificate thumbprint.

```yaml
Type: String
Parameter Sets: SingleUpdateWithThumbprint
Aliases: ClientCertificateThumbprint

Required: True
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
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### System.Collections.Hashtable
System.String
System.Boolean

## OUTPUTS

### Microsoft.Azure.Commands.ServiceFabric.Models.PsCluster

## NOTES

## RELATED LINKS

[Add-AzureRmServiceFabricClientCertificate](./Add-AzureRmServiceFabricClientCertificate.md)
