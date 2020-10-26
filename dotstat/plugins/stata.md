---
description: Connect STATA to PDH.stat with sdmxpdh
---

# STATA

![](../../.gitbook/assets/image%20%2852%29.png)

## STATA

### sdmxpdh

SDMXPDH is a version of the SDMXUSE Stata module, with the changes allowing users to connect to Pacific Data Hub .Stat API \(PDH.stat\). See the code [here](https://github.com/PacificCommunity/statasdmx).

Full credit goes to Sebastien Fontenay, Robert Picard, Nicholas Cox.

This module is a simple adaptation of the SDMXUSE module \(Fontenay\), which itself uses the MOSS module \(Picard & Cox\).

Sebastien Fontenay, 2016. "SDMXUSE: Stata module to import data from statistical agencies using the SDMX standard," Statistical Software Components S458231, Boston College Department of Economics, revised 30 Sep 2018.

Robert Picard & Nicholas J. Cox, 2011. "MOSS: Stata module to find multiple occurrences of substrings," Statistical Software Components S457261, Boston College Department of Economics, revised 29 Apr 2016.

### Installation

Instructions work for Stata SE 15.1 in Windows

Download `.ado` and `.sthlp` files from the Github repository [here](https://github.com/PacificCommunity/statasdmx).

In Stata, find your "PERSONAL" directory path with the command: `sysdir`

In Windows, go to the "PERSONAL" directory location. It is probably `C:\ado\personal\`. If the path doesn't seem to exist, make the necessary folders yourself.

Put `.ado` and `.sthlp` files inside your "PERSONAL" directory.

Restart Stata.

Check the install worked by bringing up the SDMXPDH help document: `help sdmxpdh`

### Quick start

PDH.stat resources are maintained by SPC \(Pacific Community\), so SPC is the provider for resources.

General command structure is: `sdmxpdh <resource> <provider>, <filters>`

#### See all dataflows from Pacific Data Hub

```r
sdmxpdh dataflow SPC, clear
list
```

#### Get all data for a dataflow

For example, use dataflow `DF_CPI` \(Consumer Price Index\)

```r
sdmxpdh data SPC, clear dataset(DF_CPI)
list
```

#### Get specific data for a dataflow

This time, we want `DF_CPI` time series data from 2005 to 2018, for countries Fiji and Guam.

```r
sdmxpdh data SPC, clear dataset(DF_CPI) dimensions(A.FJ+GU.INF.) start(2005) end(2018) timeseries
list
```

Using the `dimensions()` option is tricky, see the API [documentation ](../api/interface.md)for a guide.

#### Get a datastructure definition for a dataflow

Again, let's use `DF_CPI`.

```r
sdmxpdh datastructure SPC, clear dataset(DF_CPI)
list
```

