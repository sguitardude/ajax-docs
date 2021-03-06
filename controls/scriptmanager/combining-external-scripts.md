---
title: Combining External Scripts
page_title: Combining External Scripts | RadScriptManager for ASP.NET AJAX Documentation
description: Combining External Scripts
slug: scriptmanager/combining-external-scripts
tags: combining,external,scripts
published: True
position: 2
---

# Combining External Scripts



Starting with **Q1 2013 RadScriptManager** has the ability to combine external scripts (specified only by path) through the Telerik.Web.UI.WebResource.axd handler. Since this operation requires access to the project file structure, a 'safe' folder or a list of folders must be specified in the **web.config** file of the web application/site.

## Example

You can specify one or more folders from your project that host the external scripts.

>note The folder paths must be relative to the root of the application. For example, `~/path_to_folder`.
>


### Configuration

Add the following `<appSetting />` entry in your *web.config*:

````web.config
<appsettings>
	<add key="Telerik.Web.UI.ScriptsFolder" value="~/Scripts/;"/>
</appsettings>
````

This will include subfolders of the `~/scripts` folder as well, so you do not need to define them explicitly.

If you want to add several folders that are not nested within one another, add them in a single `Telerik.Web.UI.ScriptsFolder` entry:

````web.config
<appsettings>
	<add key="Telerik.Web.UI.ScriptsFolder" value="~/Scripts/;~/MoreScripts;~/Assets" />
</appsettings>
````

### Usage

Register the external scripts in **RadScriptManager**. The paths to the files can be relative to the root or to the folder containing the current page.

````ASP.NET
<telerik:RadScriptManager ID="RadScriptManager1" runat="server">
	<Scripts>
		<telerik:RadScriptReference Path="../Script1.js" />
		<telerik:RadScriptReference Path="~/Scripts/Script2.js" />
	</Scripts>
</telerik:RadScriptManager>
````



>note If a references external script is not in one of the folder designated in the configuration, it will be not be combined and will be served separately.
>


## Remarks

* You can specify more than one script folder separated by a semicolon `;`.

* The primary purpose of the control is to serve scripts from assemblies. Even when the script files are cached by the browser, when the assembly build changes, the URL generated by RadScriptManager will also change and it will serve the new script file.

* The **EnableScriptCombine** property defaults to **True**, therefore, external script files registered with RadScriptManager are combined in one WebResource file.

* A built-in cache buster is not implemented in RadScriptManager and if created manually, script files will not be combined with the rest of the resources. 

    * _**Cache buster** is a method that can be applied to resource files to force the browser request the file again from the server instead of loading it from cache. One common scenario is by using querystring in the file's path. E.g._ `/path/to/script.js?v=2`"
