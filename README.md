# Etherpad Lite Plugin for ILIAS 4.1 - 4.3 #

If you are using ILIAS 4.1 - 4.2 please use version 0.0.4 or the 'pre-43' branch: https://github.com/jrocho/ILIAS-Etherpad-Lite-Plugin/tags

If you are using ILIAS 4.3 please use version 0.0.5 or the 'master' branch: https://github.com/jrocho/ILIAS-Etherpad-Lite-Plugin/tags



## How to install: ##

### 1. Install Etherpad Lite 

   Please refer to the Etherpad Lite [installation instructions](https://github.com/Pita/etherpad-lite)

   You may use a fork of Etherpad Lite which is a version which has been tested with the
   plugin instead of office Etherpad Lite. 
   
   The fork is available at: https://github.com/jrocho/etherpad-lite
   
   Changes from the main Etherpad Lite will be merged into the fork.

*IMPORTANT: Before you start the Etherpad Lite service turn of "minify" in the settings.json otherwise the the JavaScript modifications (see section 2 of this documentation) won't take effect.*
   
   Some recommendations on this: place the Etherpad Lite server behind a reverse proxy, move it from 
   SQLite to MySQL, setup an Init script (to start the Etherpad Lite server automatically), install abiword
   for PDF/Word/OpenOffice import/export. Everything is described in the Etherpad Lite wiki on GitHub.

   I've tested this with Debian 5 (using the Debian 6 script) and Debian 6 with nginx and Apache reverse proxy
   setups. 
   
   If you want to only allow access to your pad server to ILIAS user with a session (no direct access to you pad domain)
   set
   
`"requireSession" : true,`
   
in the settings.json of Etherpad Lite
   
Set the IP address in the settings.json to 0.0.0.0
   
e.g.
   
`"ip": "0.0.0.0",`
   
   
### 2. Copy pad.js to Etherpad Lite installation

   Copy the file pad.js.sample to *"static/custom/pad.js"* within your etherpad-lite (server) folder. It removes
   the unnecessary/unused buttons from the Etherpad Lite control bar

### 3. Copy Plugin to ILIAS

   Copy the plugin files to *Customizing/global/plugins/Services/Repository/RepositoryObject/EtherpadLite/*
   in the directory structure of your ILIAS installation

### 4. Modify Plugin Configuration

Edit the file *"etherpadlite.ini.php.sample"* and rename it to *"etherpadlite.ini.php"*


`host = "pad.example.com"`
        
This is the host on which the Etherpad Lite server is running. Please note that due to JavaScript/Cookie security restrictions this has to be the same domain  as the one you're running your ILIAS installation on, or a subdomain thereof.

So if your ILIAS is running on *example.com* you can use *pad.example.com* for your etherpad host. No IP address.

`port = "9001"`

Port on which the Etherpad Lite server is listening. If you're running a reverse proxy setup this will likely be port 80.

`apikey = ""`

You API Key for Etherpad Lite. This is automatically generated when running Etherpad Lite for the first time and can be found the the Etherpad Lite directory in the file *"APIKEY.TXT"*

`defaulttext = "Willkommen bei Etherpad Lite .."` 

Default text for an Etherpad

`group = "ilias"`

You can leave this value as is. It just defines an internal group in which  Etherpad Lite users are collected.

**The group name should be only defined once with the first installation. Modifying it at a later time will prevent you from accessing the old pads.**

`domain = ".example.com"`

Set this to to top level domain with a leading dot. This is very important for the session cookies to work.

`https = "0"`
	
Turn https on or off. To use https please set this to "1"

### 5. Edit etherpad.js (only required for v0.0.5 or older versions) 

Edit the file "libs/etherpad-lite-jquery/js/etherpad.js":

Find the line 

`'host'		 : 'http://pad.example.com:9001',`

Edit this to match the host and port from the *"etherpadlite.ini.php"* file.

Also replace the http with https if you're using https

**This step is deprecated as of v0.0.6**

### 6. Enable Plugin in ILIAS 

Login to your ILIAS installation as a administrator and visit Administration -> Modules, Services and Plugins -> Administrate (on the "RepositoryObject" row (the second column of that row should already list the plugin as "EtherpadLite").

Click on "Update" and the on "Activate". The plugin should now be available and you can start to add Etherpads in you courses. You might need to  allow the creation of "Etherpad Lite" objects in your role administration.

## Updating from previous version ##

Replace the files in your ILIAS plugin directory for EtherpadLite (*Customizing/global/plugins/Services/Repository/RepositoryObject/EtherpadLite/*).

Open up the Administration Panel and navigate to the repository object plugin administration. Check if the plugin needs to be updated and please also reload the language files for the plugin.


## Changelog ##

### v0.0.6 ###

Only available for ILIAS 4.3.

* removed the need to edit the etherpad.js file
* Added preferences to disable/enable user colors, chat, line numbers and the control buttons for individual Etherpads

### v0.0.5 ###

* same as v0.0.4 but modified for ILIAS 4.3 

### v0.0.4 ###

* Updated copyright notice, removed example code, general code clean-up (latest version for ILIAS 4.2)

## Contact/Responsible ##

Jan Rocho <jan.rocho@fh-dortmund.de>

---

### This plugin uses/includes ###

Etherpad Lite PHP Client library (modified) from: 
https://github.com/TomNomNom/etherpad-lite-client

   Modified for HTTPS support

Etherpad Lite jQuery Plugin (modified) from:
https://github.com/johnyma22/etherpad-lite-jquery-plugin

   Bugfix for IE. Customization for ILIAS integration.

jQuery 1.6.2 (modified) from:
http://jquery.com/

   Fix to prevent double loading in ILIAS 4.2.

jQuery UI 1.8.16 (modified) from:
http://jqueryui.com/home

   Fix to prevent double loading if another ILIAS plugin is already using jQuery UI. 