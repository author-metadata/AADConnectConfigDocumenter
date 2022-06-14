
# Azure AD Connect Configuration Documenter

AAD Connect configuration documenter is a tool to generate documentation of an Azure AD Connect installation. Currently, the documentation is only limited to the Azure AD Connect sync configuration.

The goal of this project is to:

* To enable quick understanding of the synchronization configuration and "how it happens"!
* To build confidence in getting things right when making changes to the default configuration!!
* To know what was changed when you applied a new build / configuration of Azure AD Connect or added/updated custom sync rules!!!
 
The current capabilities of the tool include:

* Documentation of the complete configuration of Azure AD Connect sync.
* Documentation of any changes in the configuration of two Azure AD Connect sync servers or changes from a given configuration baseline.
* Generation of the PowerShell deployment script to migrate the sync rule differences or customisations from one server to another.

![Sample Report](https://github.com/Microsoft/AADConnectConfigDocumenter/wiki/Sample-Report-ToC-Contoso-Header.jpg)

Prerequisites:

1. .NET Framework 4.5 to be able to run the tool.
2. A modern browser (e.g. Microsoft Edge) to view the report.
3. A fair understanding of MIIS 2003 / ILM 2007 / FIM 2010 / MIM 2016 / AAD Sync sync engine technical concepts to be able to understand the report. A sample report generated by the tool can be found listed in the [Wiki](https://github.com/Microsoft/AADConnectConfigDocumenter/wiki/Sample-Report) section.

### **How to use the tool** (if you want to generate report for the current server installation):
1. Download the latest release AzureADConnectSyncDocumenter.zip from the [releases](https://github.com/Microsoft/AADConnectConfigDocumenter/releases) tab under the Code tab tab, UNBLOCK the downloaded zip file and extract the zip file to an empty local folder on a machine which has .NET Framework 4.5 installed.
	* This will extract the Documenter application binaries along with the sample data files for "Contoso".
	* Make sure that the tool runs by double-clicking on the cmd file AzureADConnectSyncDocumenter.cmd.
	* Upon successful execution, the generated report for "Contoso" will be found in the Documenter "Report" folder.
2. Export the Server Configuration of your Azure AD Connect sync server (named "AADC-SERVER01" in the example below) by running Get-ADSyncServerConfiguration cmdlet defined in ADSync module shipped with Azure AD Connect as in the example below.

```PowerShell

	Import-Module ADSync
	Get-ADSyncServerConfiguration -Path "C:\Temp\AADC-SERVER01-06JUN2022"

```

3. Copy the configuration export files folder produced in the previous step ("AADC-SERVER01-06JUN2022") to the "Data" directory of the Documenter tool.
4. Open a command prompt and change directory to AzureADConnectSyncDocumenter which should have AzureADConnectSyncDocumenterCmd.exe executable of the tool. Run the tool as follows to generate the report
```PowerShell

	AzureADConnectSyncDocumenterCmd.exe "AADC-SERVER01-06JUN2022" "AADC-SERVER01-06JUN2022"

```
5. Upon successful execution, the generated report will be found in the Documenter "Report" folder.

### **How to use the tool** (if you want to generate a comparison report for swing migration):
1. Download the latest release AzureADConnectSyncDocumenter.zip from the [releases](https://github.com/Microsoft/AADConnectConfigDocumenter/releases) tab under the Code tab tab, UNBLOCK the downloaded zip file and extract the zip file to an empty local folder on a machine which has .NET Framework 4.5 installed.
	* This will extract the Documenter application binaries along with the sample data files for "Contoso".
	* Make sure that the tool runs by double-clicking on the cmd file AzureADConnectSyncDocumenter.cmd.
	* Upon successful execution, the generated report for "Contoso" will be found in the Documenter "Report" folder.
2. Export the Server Configuration of your old and new Azure AD Connect sync server (named "AADC-SERVER-OLD" and "AADC-SERVER-NEW" respectively in the example below) by running Get-ADSyncServerConfiguration cmdlet defined in ADSync module shipped with Azure AD Connect as in the example below.

```PowerShell

	Import-Module ADSync
	Get-ADSyncServerConfiguration -Path "C:\Temp\AADC-SERVER-OLD-06JUN2022" # run this on the old server
	Get-ADSyncServerConfiguration -Path "C:\Temp\AADC-SERVER-NEW-06JUN2022" # run this on the new server

```

3. Copy the configuration export files folder produced in the previous step ("AADC-SERVER-OLD-06JUN2022" and "AADC-SERVER-NEW-06JUN2022") to the "Data" directory of the Documenter tool.
4. Open a command prompt and change directory to AzureADConnectSyncDocumenter which should have AzureADConnectSyncDocumenterCmd.exe executable of the tool. Run the tool as follows to generate the report
```PowerShell

	AzureADConnectSyncDocumenterCmd.exe "AADC-SERVER-OLD-06JUN2022" "AADC-SERVER-NEW-06JUN2022"

```
5. Upon successful execution, the generated report will be found in the Documenter "Report" folder.

### **How to use the tool** (if you want to generate a comparison report for in-place upgrade):
1. Download the latest release AzureADConnectSyncDocumenter.zip from the [releases](https://github.com/Microsoft/AADConnectConfigDocumenter/releases) tab under the Code tab tab, UNBLOCK the downloaded zip file and extract the zip file to an empty local folder on a machine which has .NET Framework 4.5 installed.
	* This will extract the Documenter application binaries along with the sample data files for "Contoso".
	* Make sure that the tool runs by double-clicking on the cmd file AzureADConnectSyncDocumenter.cmd.
	* Upon successful execution, the generated report for "Contoso" will be found in the Documenter "Report" folder.
2. Export the Server Configuration of your Azure AD Connect sync server (named "AADC-SERVER01" in the example below) before and after upgrade by running Get-ADSyncServerConfiguration cmdlet defined in ADSync module shipped with Azure AD Connect as in the example below.

```PowerShell

	Import-Module ADSync
	Get-ADSyncServerConfiguration -Path "C:\Temp\AADC-SERVER01-BEFORE-06JUN2022" # run this before upgrade
	Get-ADSyncServerConfiguration -Path "C:\Temp\AADC-SERVER01-AFTER-06JUN2022" # run this after upgrade
```

3. Copy the configuration export files folder produced in the previous step ("AADC-SERVER01-BEFORE-06JUN2022" and "AADC-SERVER01-AFTER-06JUN2022") to the "Data" directory of the Documenter tool.
4. Open a command prompt and change directory to AzureADConnectSyncDocumenter which should have AzureADConnectSyncDocumenterCmd.exe executable of the tool. Run the tool as follows to generate the report
```PowerShell

	AzureADConnectSyncDocumenterCmd.exe "AADC-SERVER01-AFTER-06JUN2022" "AADC-SERVER01-BEFORE-06JUN2022"

```
5. Upon successful execution, the generated report will be found in the Documenter "Report" folder.


### **How to use the tool** (if you want to generate report a comparison report for DEV Environment and PROD Environment):

1. Download the latest release AzureADConnectSyncDocumenter.zip from the [releases](https://github.com/Microsoft/AADConnectConfigDocumenter/releases) tab under the Code tab tab, UNBLOCK the downloaded zip file and extract the zip file to an empty local folder on a machine which has .NET Framework 4.5 installed.
	* This will extract the Documenter application binaries along with the sample data files for "Contoso".
	* Make sure that the tool runs by double-clicking on the cmd file AzureADConnectSyncDocumenter.cmd.
	* Upon successful execution, the generated report for "Contoso" will be found in the Documenter "Report" folder.
2. Export the Server Configuration of your DEV and PROD Azure AD Connect sync server (named "AADC-SERVER-DEV" and "AADC-SERVER-PROD" respectively in the example below) by running Get-ADSyncServerConfiguration cmdlet defined in ADSync module shipped with Azure AD Connect as in the example below.

```PowerShell

	Import-Module ADSync
	Get-ADSyncServerConfiguration -Path "C:\Temp\AADC-SERVER-DEV-06JUN2022" # run this on the DEV Environment server
	Get-ADSyncServerConfiguration -Path "C:\Temp\AADC-SERVER-PROD-06JUN2022" # run this on the PROD Environment server
```

3. Copy the configuration export files folder produced in the previous step ("AADC-SERVER-DEV-06JUN2022" and "AADC-SERVER-PROD-06JUN2022") to the "Data" directory of the Documenter tool.

4. **!!NOTE!!** _**If the names of the connector(s) do(es) not exactly match between the supplied "DEV" and "PROD" configuration files, then before running the tool, "prep" the exported config files by manually editing the xml files located in the "Connectors" folder so that the name of the connector(s) match. The name of the connector is located inside the "name" element at the start of the content.**_

5. Open a command prompt and change directory to AzureADConnectSyncDocumenter which should have AzureADConnectSyncDocumenterCmd.exe executable of the tool. Run the tool as follows to generate the report
```PowerShell

	AzureADConnectSyncDocumenterCmd.exe "AADC-SERVER-DEV-06JUN2022" "AADC-SERVER-PROD-06JUN2022" # If you want to move the changes in the DEV to PROD
	AzureADConnectSyncDocumenterCmd.exe "AADC-SERVER-PROD-06JUN2022" "AADC-SERVER-DEV-06JUN2022" # If you want to move the changes in the PROD to DEV

```
5. Upon successful execution, the generated report will be found in the Documenter "Report" folder.


### Sample report
A sample report generated by the tool can be found listed in the [Wiki](https://github.com/Microsoft/AADConnectConfigDocumenter/wiki/Sample-Report) section.

[https://aka.ms/aadConnectConfigDocumenter](https://aka.ms/aadconnectconfigdocumenter)

# Code of Conduct

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
