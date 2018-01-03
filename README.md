This documentation is to help the developers to develop against the Zimbra SOAP and Zimlet API.
It provide and offline access to both documentation and can be used in adjunction with an IDE and help the development.

This can be used with the following software :
- [Dash] (https://kapeli.com/dash) for MacOSX
- [Zeal] (https://zealdocs.org/) for Linux and Windows
and others (inc emacs and bash)

# Getting the docsets

## Dash
You will find then in the contribution section

## Zeal
You can download them using the following URL, sadly you will only have access to the latest one as Zeal only support one version of the docset installed.
If you want a previous version, you can download the tgz file and extract it in the zeal folder.

[Zimbra_SOAP_API] (https://raw.githubusercontent.com/wolfyzvf/Zimbra-Collaboration-Docset/master/build/Zimbra_SOAP_API/Zimbra_SOAP_API.xml)

[Zimbra_Zimlet_API] (https://raw.githubusercontent.com/wolfyzvf/Zimbra-Collaboration-Docset/master/build/Zimbra_Zimlet_API/Zimbra_Zimlet_API.xml)

# Build from Sources

Both docset where generated using dashing.

## Zimbra SOAP API
Get the [official documentation] (https://wiki.zimbra.com/wiki/SOAP_API_Reference_Material_Beginning_with_ZCS_8) and extract it into a new folder in the sources/Zimbra_SOAP_API/versions/

Create a new dashing.json inside with the following parameters :
```
{
    "name": "Zimbra SOAP API",  
    "package": "zimbra-soap-api",  
    "index": "index.html",  
    "selectors": {  
        "code": {  
          "type":"Command",  
          "regexp": "<(.*?)>",  
          "replacement": "$1"  
        }  
    },  
    "icon32x32": "icon.png",  
    "allowJS": false,  
    "ExternalURL": "https://wiki.zimbra.com/wiki/SOAP_API_Reference_Material_Beginning_with_ZCS_8"  
}  
```
Then build the docset with the following commands :
```
  cd sources/Zimbra_SOAP_API/versions/8.7/  
  ../../../../dashing build && tar --exclude='.DS_Store' -cvzf zimbra-soap-api.tgz zimbra-soap-api.docset  
```
Once build you can put it into a new folder in the build section.  


## Zimbra Zimlet API
Get the [official documentation] (https://wiki.zimbra.com/wiki/Zimlet_Developers_Guide:Zimbra_JavaScript_API_Reference) and extract it into a new folder in the sources/versions/

Create a new dashing.json inside with the following parameters :
```
{  
    "name": "Zimbra Zimlet API",  
    "package": "zimbra-js-api",  
    "index": "index.html",  
    "selectors": {  
        "title": {  
          "type":"Class",  
          "regexp": "Zimlet JavaScript API Reference -",  
          "replacement": ""  
        }  
    },  
    "icon32x32": "icon.png",  
    "allowJS": false,  
    "ExternalURL": "https://wiki.zimbra.com/wiki/Zimlet_Developers_Guide:Zimbra_JavaScript_API_Reference"  
}  
```
When building the the docset, use the following commands in order to delete the unnecessary index on all the pages and make it 100% compatible with dash :
```
  cd sources/Zimbra_Zimlet_API/versions/8.6/symbols/  
  sed -i '' '/\<div id="index"\>/,/\<div id="content"\>/d' symbols/*  
  mv DomQuery#init.html DomQuery%23init.html  
  ../../../../../dashing build && tar --exclude='.DS_Store' -cvzf zimbra-js-api.tgz zimbra-js-api.docset  
```
Once build you can put it into a new folder in the build section.
