---
external help file: Microsoft.Azure.Commands.ServiceFabric.dll-Help.xml
online version: 
schema: 2.0.0
---

# New-AzureRmServiceFabricCluster

## SYNOPSIS
This command uses certificates that you provide or system generated self signed certificates to set up a new service fabric cluster. The template used can be a default template or a custom template that you provide. You have the option of specifying a folder to export the self signed certificates or fetching them later from the keyvault. 

## SYNTAX

### ByExistingKeyVault
```
New-AzureRmServiceFabricCluster [-ResourceGroupName] <String> -TemplateFile <String> -ParameterFile <String>
 -SecretIdentifier <String> [-CertificateThumprint <String>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### ByNewPfxAndVaultName
```
New-AzureRmServiceFabricCluster [-ResourceGroupName] <String> -TemplateFile <String> -ParameterFile <String>
 [-PfxOutputFolder <String>] [-CertificatePassword <SecureString>] [-KeyVaultResouceGroupName <String>]
 [-KeyVaultName <String>] [-CertificateSubjectName <String>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### ByExistingPfxAndVaultName
```
New-AzureRmServiceFabricCluster [-ResourceGroupName] <String> -TemplateFile <String> -ParameterFile <String>
 -PfxSourceFile <String> [-CertificatePassword <SecureString>] [-SecondaryPfxSourceFile <String>]
 [-SecondaryCertificatePassword <SecureString>] [-KeyVaultResouceGroupName <String>] [-KeyVaultName <String>]
 [-WhatIf] [-Confirm] [<CommonParameters>]
```

### ByDefaultArmTemplate
```
New-AzureRmServiceFabricCluster [-ResourceGroupName] <String> [-PfxOutputFolder <String>]
 [-CertificatePassword <SecureString>] [-KeyVaultResouceGroupName <String>] [-KeyVaultName <String>]
 -Location <String> [-Name <String>] [-ClusterSize <Int32>] [-CertificateSubjectName <String>]
 -VmPassword <SecureString> [-OS <OperatingSystem>] [-VmSku <String>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION
The **New-AzureRmServiceFabricCluster** command uses certificates that you provide or system generated self signed certificates to set up a new service fabric cluster. The template used can be a default template or a custom template that you provide. You have the option of specifying a folder to export the self signed certificates or fetching them later from the keyvault.

If you are specifying a custom template and parameter file, you don't need to provide the certificate information in the parameter file, the system will populate these parameters.

The four options are detailed below. Scroll down for explanations of each of the parameters.

## EXAMPLES

### Specify only the cluster size, the cert subject name and the OS to deploy a cluster.

This is the simplest of all three options, and also takes in the least amount of parameter, and so is a good one if you are new to service fabric and/or just want a test cluster to deploy your applications to.

In addition to creating a new self signed cert, the command also uploads the certificate to a keyvault and uses it to deploy a secure service fabric cluster. The ClusterSize can take the values 1, 3 - 99. You can specify other optional parameters like a separate KeyVaultResouceGroupName, VmSku etc.

The OS can take four values UbuntuServer1604, WindowsServer2012R2Datacenter, WindowsServer2016Datacenter and WindowsServer2016DatacenterwithContainers. WindowsServer2016Datacenter is the default.

The default VM user id is adminuser.

```
New-AzureRmServiceFabricCluster [-ResourceGroupName] <String> [-PfxOutputFolder <String>]
 [-CertificatePassword <SecureString>] [-KeyVaultResouceGroupName <String>] [-KeyVaultName <String>]
 -Location <String> [-Name <String>] [-ClusterSize <Int32>] [-CertificateSubjectName <String>]
 -VmPassword <SecureString> [-OS <OperatingSystem>] [-VmSku <String>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

Here is a filled out example to deploy a 3 node cluster. The certificate is saved to the $pfxfolder and is named $RGname+Timestamp.pfx. 
```
$pwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
$RGname="chacko09"
$clusterloc="SouthCentralUS"
$subname="$RGname.$clusterloc.cloudapp.azure.com"
$pfxfolder="c:\Mycertificates\"

Write-Output "create cluster in " $clusterloc "subject name for cert " $subname "and output the cert into " $pfxfolder

New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize 3 -VmPassword $pwd -CertificateSubjectName $subname -PfxOutputFolder $pfxfolder -CertificatePassword $pwd

```


### Specify an existing Certificate resource in Keyvault and a custom template to deploy a cluster 

Use this command, when you want to reuse a certificate that has already been uploaded to your keyvault.

```
New-AzureRmServiceFabricCluster [-ResourceGroupName] <String> -TemplateFile <String> -ParameterFile <String>
 -SecretIdentifier <String> [-CertificateThumprint <String>] [-WhatIf] [-Confirm] [<CommonParameters>]
```
Here is a filled out example of the above command
```
$RGname="chacko20"
$templateParmfile="C:\Users\chackdan\Documents\GitHub\azure-quickstart-templates-parms\service-fabric-secure-nsg-cluster-65-node-3-nodetype\azuredeploytest.parameters.json"
$templateFile="C:\Users\chackdan\Documents\GitHub\azure-quickstart-templates\service-fabric-secure-nsg-cluster-65-node-3-nodetype\azuredeploy.json"
$secertId="https://chackokv1.vault.azure.net:443/secrets/chackdantestcertificate4/56ec774dc61a462bbc645ffc9b4b225f"


New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -TemplateFile $templateFile -ParameterFile $templateParmfile -SecretIdentifier $secertId 
```

### Create a new cluster using a custom template, Specify the different RG name for the keyvault and have the system upload the certificate to it 

Use this command when you want to set up the keyvault in a different RG than the cluster. The system will generate a self signed cert based on the parameters you specify.

```
New-AzureRmServiceFabricCluster [-ResourceGroupName] <String> -TemplateFile <String> -ParameterFile <String>
 [-PfxOutputFolder <String>] [-CertificatePassword <SecureString>] [-KeyVaultResouceGroupName <String>]
 [-KeyVaultName <String>] [-CertificateSubjectName <String>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

Here is a filled out example of the above command

```
$pwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
$RGname="chacko20"
$keyVaultRG="chacko20kvrg"
$keyVault="chacko20kv"
$clusterloc="SouthCentralUS"
$subname="$RGname.$clusterloc.cloudapp.azure.com"
$pfxfolder="c:\Mycertificates\"
$templateParmfile="C:\Users\chackdan\Documents\GitHub\azure-quickstart-templates-parms\service-fabric-secure-nsg-cluster-65-node-3-nodetype\azuredeploytest.parameters.json"
$templateFile="C:\Users\chackdan\Documents\GitHub\azure-quickstart-templates\service-fabric-secure-nsg-cluster-65-node-3-nodetype\azuredeploy.json"
$secertId="https://chackokv1.vault.azure.net:443/secrets/chackdantestcertificate4/55ec7c4dc61a462bbc645ffc9b4b225f"
$thumprint="C2D7E11DD35153A702A51D10A424A3014B9B6E8B"

New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -TemplateFile $templateFile -ParameterFile $templateParmfile -PfxOutputFolder $pfxfolder -CertificatePassword $pwd -KeyVaultResouceGroupName $keyVaultRG  -KeyVaultName $keyVault -CertificateSubjectName $subname
```

### Bring your own Certificate and custom template and create a new cluster

Use this command when you already have an existing certificate (that you have generated or have bought from a CA), and want that to be uploaded to a seperate new or existing Keyvault RG and have the system create the cluster. 

```
New-AzureRmServiceFabricCluster [-ResourceGroupName] <String> -TemplateFile <String> -ParameterFile <String>
 -PfxSourceFile <String> [-CertificatePassword <SecureString>] [-SecondaryPfxSourceFile <String>]
 [-SecondaryCertificatePassword <SecureString>] [-KeyVaultResouceGroupName <String>] [-KeyVaultName <String>]
 [-WhatIf] [-Confirm] [<CommonParameters>]
```

Here is a filled out example of the above command

```
$certPwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
$RGname="chacko20"
$keyVaultRG="chacko20kvrg"
$keyVault="chacko20kv"
$clusterloc="SouthCentralUS"
$pfxsourcefile="c:\Mycertificates\my2017Prodcert.pfx"
$templateParmfile="C:\Users\chackdan\Documents\GitHub\azure-quickstart-templates-parms\service-fabric-secure-nsg-cluster-65-node-3-nodetype\azuredeploytest.parameters.json"
$templateFile="C:\Users\chackdan\Documents\GitHub\azure-quickstart-templates\service-fabric-secure-nsg-cluster-65-node-3-nodetype\azuredeploy.json"

New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -TemplateFile $templateFile -ParameterFile $templateParmfile -PfxSourceFile $pfxsourcefile -CertificatePassword $certpwd -KeyVaultResouceGroupName $keyVaultRG -KeyVaultName $keyVault 

```

## PARAMETERS

### -CertificatePassword
The password for the pfx file.

```yaml
Type: SecureString
Parameter Sets: ByNewPfxAndVaultName, ByExistingPfxAndVaultName, ByDefaultArmTemplate
Aliases: CertPassword

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -CertificateSubjectName
The certificate common name of the certificate to be created.

```yaml
Type: String
Parameter Sets: ByNewPfxAndVaultName, ByDefaultArmTemplate
Aliases: Subject

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -CertificateThumprint
The thumbprint for the Azure key vault secret.

```yaml
Type: String
Parameter Sets: ByExistingKeyVault
Aliases: Thumbprint

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -ClusterSize
The size of the cluster, the default is 5 nodes.

```yaml
Type: Int32
Parameter Sets: ByDefaultArmTemplate
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Confirm
Confirmation prompt.

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

### -KeyVaultName
Azure key vault name 

```yaml
Type: String
Parameter Sets: ByNewPfxAndVaultName, ByExistingPfxAndVaultName, ByDefaultArmTemplate
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -KeyVaultResouceGroupName
Azure key vault resource group name

```yaml
Type: String
Parameter Sets: ByNewPfxAndVaultName, ByExistingPfxAndVaultName, ByDefaultArmTemplate
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Location
The resource group location

```yaml
Type: String
Parameter Sets: ByDefaultArmTemplate
Aliases: 

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Name
The name of the cluster. If not specified, it is defaulted to the same as the resource group name.
```yaml
Type: String
Parameter Sets: ByDefaultArmTemplate
Aliases: ClusterName

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -OS
The Operating System of the VMs that make up the cluster.

```yaml
Type: OperatingSystem
Parameter Sets: ByDefaultArmTemplate
Aliases: 
Accepted values: WindowsServer2012R2Datacenter, WindowsServer2016Datacenter, WindowsServer2016DatacenterwithContainers, UbuntuServer1604

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -ParameterFile
The path of the template parameter file.

```yaml
Type: String
Parameter Sets: ByExistingKeyVault, ByNewPfxAndVaultName, ByExistingPfxAndVaultName
Aliases: 

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -PfxOutputFolder
The folder where the new certifcate needs to be created.

```yaml
Type: String
Parameter Sets: ByNewPfxAndVaultName, ByDefaultArmTemplate
Aliases: Destination

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -PfxSourceFile
The path to the existing Pfx file. For example "c:\mycerts\mycert.pfx"

```yaml
Type: String
Parameter Sets: ByExistingPfxAndVaultName
Aliases: Source

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
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -SecondaryCertificatePassword
The password of the secondary certificate file

```yaml
Type: SecureString
Parameter Sets: ByExistingPfxAndVaultName
Aliases: SecCertPassword

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -SecondaryPfxSourceFile
The path to the existing Pfx file. For example "c:\mycerts\mycert.pfx"

```yaml
Type: String
Parameter Sets: ByExistingPfxAndVaultName
Aliases: SecSource

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -SecretIdentifier
The existing Azure key vault secret uri. For example "https://chackokv1.vault.azure.net:443/secrets/chackdantestcertificate4/55ec7c4dc61a462bbc645ffc9b4b225f".

```yaml
Type: String
Parameter Sets: ByExistingKeyVault
Aliases: 

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -TemplateFile
The path to the template file.

```yaml
Type: String
Parameter Sets: ByExistingKeyVault, ByNewPfxAndVaultName, ByExistingPfxAndVaultName
Aliases: 

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -VmPassword
The password of the VM for SSH/RDP.

```yaml
Type: SecureString
Parameter Sets: ByDefaultArmTemplate
Aliases: 

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -VmSku
The Vm Sku.

```yaml
Type: String
Parameter Sets: ByDefaultArmTemplate
Aliases: Sku

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -WhatIf
Shows what would happen if the cmdlet runsvs not.

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

### System.String
Microsoft.Azure.Management.ResourceManager.Models.DeploymentMode

## OUTPUTS

## NOTES

## RELATED LINKS

[Get-AzureRmServiceFabricCluster](./Get-AzureRmServiceFabricCluster.md)
[Add-AzureRmServiceFabricClusterCertificate](./Add-AzureRmServiceFabricClusterCertificate.md)
[Add-AzureRmServiceFabricApplicationCertificate](./Add-AzureRmServiceFabricApplicationCertificate.md)
