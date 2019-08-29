# Liferay Language Plugin Ext

*liferay-language-plugin-ext*

## Overview

Liferay Portal 6.1 Ext plugin that overrides Liferay's LanguageUtil.updateCookie method.

Specifically, it adds a 2nd language_id cookie (GUEST_LANGUAGE_ID_EXT) with a domain specified by the *session.cookie.domain* portal property.


## Supported Products

* Liferay Portal 6.1 EE GA2 (6.1.20+)


## Configuration

### Configure Portal Properties

Add/update the following property in the plugin's [portal-ext.properties](docroot/WEB-INF/ext-impl/src/portal-ext.properties) file or in "LIFERAY_HOME/portal-ext.properties":

| *Property* | *Description* |
| :------------- | :------------- |
| session.cookie.domain | Domain of the 2nd language_id cookie. |


### Sample Portal Properties

```
#
# The login process sets several cookies if persistent cookies are enabled.
# Set this property to set the domain of those cookies.
#
session.cookie.domain=.example.com
```


## Building

Step 1. Checkout source from GitHub project to a Liferay Portal Plugins SDK

    % cd LIFERAY_PORTAL_PLUGINS_SDK/ext
    % git clone https://github.com/pmercer/liferay-language-plugin-ext 

Step 2. Build and package

    % ant clean war

This will build "liferay-language-plugin-ext-A.B.C.D.war" in the Liferay Portal plugins SDK dist folder.

NOTE: Requires JDK 1.6+ and Liferay Portal Plugins SDK.


## Deployment

### Deploy to Liferay Portal + Apache Tomcat Bundle

* Deploy "liferay-language-plugin-ext-A.B.C.D.war" to "LIFERAY_HOME/deploy" folder.
* Start Liferay Portal to install EXT plugin.
* Stop Liferay Portal.
* Start Liferay Portal again to use EXT plugin.


## Verfication

### Expected Results

Should see the following messages in the server log at startup and/or when toggling between the different language icons in the Liferay language portlet:

```
*** adding Cookie
[name=GUEST_LANGUAGE_ID, value=en_US, domain=null]
*** adding Cookie
[name=GUEST_LANGUAGE_ID_EXT, value=en_US, domain=.example.com]
```


## Credit

Many thanks to Minhchau Dang's helpful guidance to my questions on the *Liferay extending LanguageUtil.get() method* thread on the Liferay dev forum.
