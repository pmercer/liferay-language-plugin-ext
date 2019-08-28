# Liferay Language Plugin Ext

*liferay-language-plugin-ext*

## Overview

Liferay Portal 6.1 Ext plugin that overrides Liferay's LanguageImpl.updateCookie method.

Specifically, it adds a 2nd language_id cookie (GUEST_LANGUAGE_ID_EXT) with a parent domain of ".example.com".


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

Should see the following messages in the server log at startup and when toggling between the different language icons in the Liferay language portlet:

```
*** adding Cookie
[name=GUEST_LANGUAGE_ID, value=en_US, domain=null]
*** adding Cookie
[name=GUEST_LANGUAGE_ID_EXT, value=en_US, domain=.example.com]
```

### Actual Results

Seeing the following ERROR message in the server log at startup:

```
ERROR [LiferayMethodExceptionEventHandler:34] java.lang.NullPointerException
java.lang.NullPointerException
        at com.example.LanguageResources._loadLocale(LanguageResources.java:155)
        at com.example.LanguageResources.getMessage(LanguageResources.java:81)
        at com.example.MyCustomLanguageImpl.get(MyCustomLanguageImpl.java:366)
        at com.example.MyCustomLanguageImpl.get(MyCustomLanguageImpl.java:353)
```
