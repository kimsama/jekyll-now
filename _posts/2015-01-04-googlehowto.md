---
layout: post
title: Unity-QuickSheet with Google Spreadsheet Howto
categories: []
tags: [QuickSheet]
published: True

---

## How to work with Google Spreadsheet

This post shows and helps you how to set up and use [Unity-QuickSheet](https://github.com/kimsama/Unity-QuickSheet) with Google Spreadsheet. 

![Google New Setting File]({{ site.baseurl }}/images/google_spreadsheet.png)

First, you need to create a google spreadsheet on your Google Drive. Login your Google Drive with your google account and create a new spreadsheet.

Change the title of the created spreadsheet as *'MySpreadSheet'* like the following:

![Create a google spreadsheet]({{ site.baseurl }}/images/gdata_title.png "Google Spreadsheet")

Next, create a new worksheet and rename it to whatever you want to as the following image shows:

![Create a worksheet]({{ site.baseurl }}/images/gdata_worksheet.png "Google Worksheet")

Now, it needs to edit cells for spreadsheet. Insert *'Key'* and *'Text'* at the first row of the created worksheet as like that:

![Edit cells]({{ site.baseurl }}/images/gdata_cells.png)

**IMPORTANT** <br>
Note that the first row should not contain any values which are used for your class members.


## Google OAuth2 Service Account ##

Before futher going, you need to create *'Google OAuth2 Account'* to verity your account and make Unity available to access on your google spreadsheet. 

See the [OAuth2 Service Account](https://opendatakit.org/use/aggregate/oauth2-service-account/) article to create *'Google OAuth2 Service Account'*. One thing to note is that you should create json type of private key not the p12 one for Unity-Quicksheet.

If you successfully get the json private key then select *'GoogleDataSettings.asset'* file which can be found under *'Assets/QuickSheet/GDataPlugin/Editdor'* folder. 

![GoogleDataSettings.asset]({{ site.baseurl }}/images/google-setting.png)

1. First, set the downloaded json private key to the *'JSON File'*.
2. Now, 2)*'Client ID'* and 3)*'Client Secret'* will be automatically sepcified
3. Click *'Start Authentication'* button it will launch your browser. 

![GoogleDataSettings.asset]({{ site.baseurl }}/images/google-accesscode-01.png)

Select 'Allow' then go to next.

![GoogleDataSettings.asset]({{ site.baseurl }}/images/google-accesscode.png)

Now you will see the *'access code'*. Copy it and paste to the Unity's 4)*'Access Code'* setting

Final step is to click 'Finish Authenticate' button. 

Set other paths 'Runtime Path' and 'Editor Path' for your project.


### Step 1) Creating Google Spreadsheet Setting File 

First you need thing to do is creating a google spreadsheet setting file. Simply right click on the Project view and select *'Create > Spreadsheet Tools > Google'*. It creates a new file which shows various setting to create script files and get data from the specified google spreadsheet.

![Google Create Setting File Menu]({{ site.baseurl }}/images/google_create_spreadsheettools.png)


Select ***Google*** menu item then it creates setting file. It may be shown like the following:

![Google New Setting File]({{ site.baseurl }}/images/google_new_setting.png)

#### GoogleDrive Setting

1. Speicify your google account.
2. Sepecify your password for the account.

#### Script Path Setting

3. ***Template*** indicates a path where template files which are neccessary to generate script files.  In most case you don't need to change it.
4. ***Runtime*** indicates a path where generated script files which are used on runtime will be put.
5. ***Editor*** inidicates a path where generated script files which are used on editor mode will be put.
6. ***Spread Sheet Name*** is what the name of the spreadsheet which is created on google drive.
7. ***Work Sheet Name*** is one of the worksheet name of the spreadwheet you want to get data from.

After doing done with all path setting, press ***Import*** button then it shows all column headers of the page. That are neccessary to let you set the type of the each cells.

![Google New Setting File]({{ site.baseurl }}/images/google_type_setting.png)

Set the proper type of the cells.

Currently the following types are supoorted:

- string
- int
- float
- double
- enum
- bool

### Step 2) Generating Script Files

If you've done all necessary setting, it's time to generate some script files which are needed for reading data in from the sheet page of the excel file and to store that within *ScriptableObject* which is being as an asset file in the *Project View*.

Press ***Generate*** button.

After generating some script files, Unity Editor starts to compile those. Wait till Unity ends doing compile then check the specified *Editor* and *Runtime* paths all necessary script files are correctly generated. 

In ***Editor*** folder should have contain two files:

* *your-sheetpage-name*AssetCreator.cs
* *your-sheetpage-name*Editor.cs

In ***Runtime*** foller should have contain tow files:
    
* *your-sheetpag-name*.cs
* *your-sheetpage-name*Data.cs

See the *your-sheetpage-name*Data.cs file. The class members of the file represent each cells of the sheet page.

{% highlight csharp %}
using UnityEngine;
using System.Collections;

///
/// !!! Machine generated code !!!
/// !!! DO NOT CHANGE Tabs to Spaces !!!
///
[System.Serializable]
public class PlayerItemData
{
	[SerializeField]
	string key;
	
	[ExposeProperty]
	public string Key { get {return key; } set { key = value;} }
	
	[SerializeField]
	string text;
	
	[ExposeProperty]
	public string Text { get {return text; } set { text = value;} }
{% endhighlight %}

### Step 3) Importing Spreadsheet Data

Now you need to create an asset file which will imports and stores all data from google drive. Simply right click on the Project view and select *'Create > Google'*. Now there is a new menu item which has same name with the worksheet name of the google spreadsheet.

![Google New Setting File]({{ site.baseurl }}/images/google_spreadsheet_assetfile.png)

Select the menu item then it creates an asset file. It may be shown like the following:

![Google New Setting File]({{ site.baseurl }}/images/google_created_assetfile.png)

Note that the created asset file has same file name as the specified worksheet name.

1. Type ***Username*** and ***Password*** of your google account.
2. Specify the same Spreadsheet and Worksheet name as the google setting.
3. Press ***Download*** button then it starts to import data from google drive. (It may takes a few seconds.)

Finished downloading shows the imported data on the Inspector View like the following:

![Google New Setting File]({{ site.baseurl }}/images/google_imported_data.png)

It's done. Hope you enjoy that!


## TroubleShoting

### Invalid Credential Error

If you met an error which is shown as an invalid credentials when you try to get data by clicking 'download' button, check that your google accout page and you have two-stage verification.

If you have Google two-stage verification on, then it doesn't matter what your Google password is, it won't be accepted. You need to generate (on Google) what is called an Application Specific Password (ASP). Go to [Google Account Page](https://www.google.com/settings/account) and set up an ASP, enter the password you generate as the password in your code, and you're done.

### Security Error 

Google Spreadsheet plugin does not work in the Unity web player's security sandbox. You should change the *Platform* to *'Stand Alone'* or something else such as *'iOS'* or *'Android'* platform in the ***Build Setting***.

