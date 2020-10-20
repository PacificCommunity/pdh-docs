# STATA

  
&lt;!--  
 /\* Font Definitions \*/  
 @font-face  
	{font-family:"Cambria Math";  
	panose-1:2 4 5 3 5 4 6 3 2 4;  
	mso-font-charset:0;  
	mso-generic-font-family:roman;  
	mso-font-pitch:variable;  
	mso-font-signature:3 0 0 0 1 0;}  
@font-face  
	{font-family:Calibri;  
	panose-1:2 15 5 2 2 2 4 3 2 4;  
	mso-font-charset:0;  
	mso-generic-font-family:swiss;  
	mso-font-pitch:variable;  
	mso-font-signature:-469750017 -1073732485 9 0 511 0;}  
 /\* Style Definitions \*/  
 p.MsoNormal, li.MsoNormal, div.MsoNormal  
	{mso-style-unhide:no;  
	mso-style-qformat:yes;  
	mso-style-parent:"";  
	margin-top:0cm;  
	margin-right:0cm;  
	margin-bottom:8.0pt;  
	margin-left:0cm;  
	line-height:107%;  
	mso-pagination:widow-orphan;  
	font-size:11.0pt;  
	font-family:"Calibri",sans-serif;  
	mso-ascii-font-family:Calibri;  
	mso-ascii-theme-font:minor-latin;  
	mso-fareast-font-family:Calibri;  
	mso-fareast-theme-font:minor-latin;  
	mso-hansi-font-family:Calibri;  
	mso-hansi-theme-font:minor-latin;  
	mso-bidi-font-family:"Times New Roman";  
	mso-bidi-theme-font:minor-bidi;  
	mso-fareast-language:EN-US;}  
.MsoChpDefault  
	{mso-style-type:export-only;  
	mso-default-props:yes;  
	font-family:"Calibri",sans-serif;  
	mso-ascii-font-family:Calibri;  
	mso-ascii-theme-font:minor-latin;  
	mso-fareast-font-family:Calibri;  
	mso-fareast-theme-font:minor-latin;  
	mso-hansi-font-family:Calibri;  
	mso-hansi-theme-font:minor-latin;  
	mso-bidi-font-family:"Times New Roman";  
	mso-bidi-theme-font:minor-bidi;  
	mso-fareast-language:EN-US;}  
.MsoPapDefault  
	{mso-style-type:export-only;  
	margin-bottom:8.0pt;  
	line-height:107%;}  
@page WordSection1  
	{size:595.3pt 841.9pt;  
	margin:70.85pt 70.85pt 70.85pt 70.85pt;  
	mso-header-margin:35.4pt;  
	mso-footer-margin:35.4pt;  
	mso-paper-source:0;}  
div.WordSection1  
	{page:WordSection1;}  
--&gt;  


**STATA**

‌

**sdmxpdh**

‌

SDMXPDH is a version of the SDMXUSE Stata module, with the changes allowing users to connect to Pacific Data Hub .Stat API \(PDH.STAT\).

‌

Full credit goes to Sebastien Fontenay, Robert Picard, Nicholas Cox.

‌

This module is a simple adaptation of the SDMXUSE module \(Fontenay\), which itself uses the MOSS module \(Picard & Cox\).

‌

Sebastien Fontenay, 2016. "SDMXUSE: Stata module to import data from statistical agencies using the SDMX standard," Statistical Software Components S458231, Boston College Department of Economics, revised 30 Sep 2018.

‌

Robert Picard & Nicholas J. Cox, 2011. "MOSS: Stata module to find multiple occurrences of substrings," Statistical Software Components S457261, Boston College Department of Economics, revised 29 Apr 2016.

‌

**Installation**

‌

Instructions work for Stata SE 15.1 in Windows

‌

Download .ado and .sthlp files from the repo

‌

In Stata, find your "PERSONAL" directory path with the command: sysdir

‌

In Windows, go to the "PERSONAL" directory location. It is probably C:\ado\personal\. If the path doesn't seem to exist, make the necessary folders yourself.

‌

Put .ado and .sthlp files inside your "PERSONAL" directory.

‌

Restart Stata.

‌

Check the install worked by bringing up the SDMXPDH help document: help sdmxpdh

‌

**Quick start**

‌

PDH.STAT resources are maintained by SPC \(Pacific Community\), so SPC is the provider for resources.

‌

General command structure is: sdmxpdh &lt;resource&gt; &lt;provider&gt;, &lt;filters&gt;

‌

**See all dataflows from Pacific Data Hub**

‌

sdmxpdh dataflow SPC, clear

‌

list

‌

**Get all data for a dataflow**

‌

For example, use dataflow DF\_CPI \(Consumer Price Index\)

‌

sdmxpdh data SPC, clear dataset\(DF\_CPI\)

‌

list

‌

**Get specific data for a dataflow**

‌

This time, we want DF\_CPI time series data from 2005 to 2018, for countries Fiji and Guam.

‌

sdmxpdh data SPC, clear dataset\(DF\_CPI\) dimensions\(.FJ+GU.\_T.....GY\) start\(2005\) end\(2018\) timeseries

‌

list

‌

Using the dimensions\(\) option is tricky, see the API documentation for a guide \([https://sdd-dotstat-api-gateway.portal.azure-api.net/docs/services/pdh-stat-api/operations/get-data-flow-key-provider?&groupBy=tag](https://sdd-dotstat-api-gateway.portal.azure-api.net/docs/services/pdh-stat-api/operations/get-data-flow-key-provider?&groupBy=tag)\).

‌

**Get a datastructure definition for a dataflow**

‌

Again, let's use DF\_CPI.

‌

sdmxpdh datastructure SPC, clear dataset\(DF\_CPI\)

‌

list

‌

**Download**

‌

[Download plugin via GitHub repository](https://github.com/PacificCommunity/statasdmx#sdmxpdh)

‌

**Python**

‌

\[Denis/Conor to add\]

‌

Under development

