# firefox

Control Mozilla Firefox.

## `about:config` Overrides

Disable user-hostile "what's new" page:

* `browser.startup.homepage_override.mstone` set to `ignore`
  * https://kb.mozillazine.org/Browser.startup.homepage_override.mstone
  * Detecting that an update has occured to open a page at startup
  * When a user starts up their browser, this preference is examined. If its value differs from the browser’s current milestone, then the user is redirected to the homepage specified in startup.homepage_override_url and this preference’s value is updated to the current milestone.

* `startup.homepage_override_url` set to `about:blank`
  * https://kb.mozillazine.org/Startup.homepage_override_url
  * When a user starts up their browser after upgrading (i.e., if browser.startup.homepage_override.mstone is different than the last time the browser started), the URL specified in this preference is loaded instead of their homepage

Disable remote extension blocking on '[quarantined](https://support.mozilla.org/en-US/kb/quarantined-domains)' domains:

* `extensions.quarantinedDomains.enabled` set to `false`
