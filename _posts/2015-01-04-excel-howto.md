---
layout: post
title: Unity-QuickSheet with Excel Howto
categories: []
tags: [QuickSheet]
published: True

---

## How to work with Excel

This post shows and helps you how to set up and use [Unity-QuickSheet](https://github.com/kimsama/Unity-QuickSheet) with excel. 

![Sample Excel file]({{ site.baseurl }}/images/excel_sample.png)

Before starting, check your spreadsheet page again. It should start without an empty row which means the first row should not be an empty one.


### Step 1) Create Excel setting file

First you need thing to do is creating an excel stting file. Simply right click on the Project view and select *'Create > Spreadsheet Tools > Excel'*. It creates a new file which shows various setting to create script files and get data from the specified excel file.

![Create Setting File]({{ site.baseurl }}/images/create_excel_setting.png)

Select ***Excel*** mene item then it creates setting file. It may be shown like the following:

![Excel Setting]({{ site.baseurl }}/images/excel_new_setting.png)

Let's start to do settinig.

#### File Setting

File setting is setting for what excel file and its sheet page to import.
![Excel Setting]({{ site.baseurl }}/images/excel_file_setting.png)

First you should specify what excel file to import.

1. Select an excel file to import with **File Open Dialog**.

An excel file can have one or more sheet pages so you need to decide what sheet you select and retrieve data from. 

2. Select a sheet page you want to import.

3. Press ***Import*** button imports the specified excel file and shows all column headers.

#### Type Setting

Importing the specified sheet page shows all column headers of the page. That are neccessary to let you set the type of the each cells.

![Excel Setting]({{ site.baseurl }}/images/excel_type_setting.png)

Set the proper type of the cells.

Currently the following types are supoorted:

- string
- int
- float
- double
- enum
- bool


#### Path Setting

Path setting are concerned with specifying paths where the generated script files are put.

***Note:*** All paths should be relative without 'Assets/'.`

![Excel Setting]({{ site.baseurl }}/images/excel_path_setting.png)

1. ***Template*** indicates a path where template files which are neccessary to generate script files.  In most case you don't need to change it.
2. ***Runtime*** indicates a path where generated script files which are used on runtime will be put.
3. ***Editor*** inidicates a path where generated script files which are used on editor mode will be put.

### Step 2) Generating script files

If you've done all necessary setting, it's time to generate some script files which are needed for reading data in from the sheet page of the excel file and to store that within *ScriptableObject* which is being as an asset file in the *Project View*.

Press ***Generate*** button.

After generating some script files, Unity Editor starts to compile those. Wait till Unity ends doing compile then check the specified *Editor* and *Runtime* paths all necessary script files are correctly generated. 

In ***Editor*** folder should have contain two files:

* *your-sheetpage-name*AssetPostProcessor.cs
* *your-sheetpage-name*Editor.cs

In ***Runtime*** foller should have contain tow files:
    
* *your-sheetpag-name*.cs
* *your-sheetpage-name*Data.cs

See the *your-sheetpage-name*Data.cs file. The class members of the file represent each cells of the sheet page.

`(put example data class code here)`



### Step 3) Import spreadsheet data

Creating asset file and importing data from the spreadsheet file into that created asset file is done just by simply doing reimport any *xls* or *xlsx* file within Project view.

![Excel Setting]({{ site.baseurl }}/images/excel_reimport.png)

Reimporting *xls* or *xlsx* file will automatically create an asset file which has same file name as the sheet page name(*not excel file name*) and automatically import data from the sheet page of the excel file into the created asset file. 

![Asset file]({{ site.baseurl }}/images/excel_imported.png)

It's done. Hope you enjoy that!

## TroubleShoting

`(more will be later...)`
