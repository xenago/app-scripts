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

Disable update popup:

* `app.update.doorhanger` set to `false`

Disable showing 'suggested sites' nonsense (Wikipedia, Facebook, Twitter, YouTube etc.):

* `browser.urlbar.suggest.topsites` set to `false`

Disable remote extension blocking on '[quarantined](https://support.mozilla.org/en-US/kb/quarantined-domains)' domains:

* `extensions.quarantinedDomains.enabled` set to `false`

On Developer version only, disable addon signing:

* `xpinstall.signatures.required` set to `false`

## Load unsigned addons

Mozilla is an unethical company that tries to prevent users from running their own code, and gaslights users to try to convince them that ad tracking is for their own benefit.

Temporary: go to [about:debugging#/runtime/this-firefox](about:debugging#/runtime/this-firefox) to load `manifest.json` from unpacked zip

Permanent: use firefox developer with above tweak to `xpinstall.signatures.required`.

# Install magnolia1234's Bypass Paywalls Clean

Installation: https://github.com/bpc-clone/bypass-paywalls-firefox-clean?tab=readme-ov-file#installation

1. Download `*-custom.xpi` file from [GitFlic releases page](https://gitflic.ru/project/magnolia1234/bpc_uploads)
2. Enable the debug menu (`Settings` > `About` > tap Firefox logo 5 times > return to settings > `Install extension from file`).
