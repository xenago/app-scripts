# firefox

Control Mozilla Firefox.

## Prevent automatic downloads from saving

1. In `about:preferences#general` under `Files and Applications`, select `Always ask you where to save files`
2. Scroll a bit lower down to `Applications` and locate `What should Firefox do with other files?` - set this to  `Ask whether to open or save files`

## `about:config` Overrides

Disable user-hostile "what's new" page:

* `browser.startup.homepage_override.mstone` set to `ignore`
  * https://kb.mozillazine.org/Browser.startup.homepage_override.mstone
  * Detecting that an update has occured to open a page at startup
  * When a user starts up their browser, this preference is examined. If its value differs from the browser’s current milestone, then the user is redirected to the homepage specified in startup.homepage_override_url and this preference’s value is updated to the current milestone.

* `startup.homepage_override_url` set to `about:blank`
  * https://kb.mozillazine.org/Startup.homepage_override_url
  * When a user starts up their browser after upgrading (i.e., if browser.startup.homepage_override.mstone is different than the last time the browser started), the URL specified in this preference is loaded instead of their homepage

Disable AI-ML chatbot

* `browser.ml.chat.enabled` set to `false`
* Disable the sidebar in Settings

Disable AI-ML link preview

* `browser.ml.linkPreview` set to `false`

Restore ability to add custom search engines (a particularly ridiculous move by Mozilla):

* `browser.urlbar.update2.engineAliasRefresh` set to `true`

Disable showing 'suggested sites' nonsense (Wikipedia, Facebook, Twitter, YouTube etc.):

* `browser.urlbar.suggest.topsites` set to `false`

Disable OHTTP nonsense:

* `network.trr.use_ohttp` set to `false`
* `network.trr.ohttp.config_uri` set to nothing
* `network.trr.ohttp.relay_uri` set to nothing

Disable remote extension blocking on '[quarantined](https://support.mozilla.org/kb/quarantined-domains)' domains:

* `extensions.quarantinedDomains.enabled` set to `false`

Improve clipboard support (useful with e.g. Apache Guacamole):

* `dom.events.asyncClipboard.readText` set to `true`
* `dom.events.testing.asyncClipboard` set to `true`

On Developer version only, disable addon signing:

* `xpinstall.signatures.required` set to `false`

* The following `about:config` options are **PLACEBOS AND SHOULD BE AVOIDED**
  * `app.update.doorhanger` set to `false`
  * `app.update.silent` set to `true`

## `policies.json` Overrides

Disable automatic updates (holy hell they are irritating, it is as though the browser is designed to kill productivity):

* [Copy](https://support.mozilla.org/en-US/kb/customizing-firefox-using-policiesjson) `policies.json` to one of these `distribution` directories (create if it does not exist), based on OS:
  * `C:\Program Files\Mozilla Firefox\distribution`
    * Or for local install, `%LOCALAPPDATA%\Mozilla Firefox\distribution`
  * `Firefox.app/Contents/Resources/distribution`
  * `/etc/firefox/policies` or `firefox/distribution`
## Mozilla-hosted addons

* Block ads: [uBlock Origin](https://addons.mozilla.org/firefox/addon/ublock-origin/)
* Block sponsors embedded in YouTube videos: [SponsorBlock](https://addons.mozilla.org/firefox/addon/sponsorblock/)
* Spoof Chrome to trick badware sites into loading: [Chrome Mask](https://addons.mozilla.org/firefox/addon/chrome-mask/)
* Fix awful Wikipedia UI without logging in: [Classic mode for Wikipedia](https://addons.mozilla.org/firefox/addon/classic-wikipedia/)
* Fix awful Reddit UI without manually going to old subdomain: [Old Reddit Redirect](https://addons.mozilla.org/en-CA/firefox/addon/old-reddit-redirect/)

## Load unsigned addons

Mozilla is an unethical company that tries to prevent users from running their own code, and gaslights users to try to convince them that ad tracking is for their own benefit.

Temporary: go to [about:debugging#/runtime/this-firefox](about:debugging#/runtime/this-firefox) to load `manifest.json` from unpacked zip

Permanent: use firefox developer with above tweak to `xpinstall.signatures.required`.

## Install magnolia1234's Bypass Paywalls Clean

Installation info: https://github.com/bpc-clone/bypass-paywalls-firefox-clean?tab=readme-ov-file#installation

1. Download `*-custom.xpi` file from [GitFlic releases page](https://gitflic.ru/project/magnolia1234/bpc_uploads)
2. On Desktop, use the cog in the top-right of the extensions page to install the addon from the downloaded file.
3. On Android, enable the debug menu (`Settings` > `About` > tap Firefox logo 5 times > return to settings > `Install extension from file`).

## Install without Administrator privileges

It is possible to install the local single-user Firefox alongside the global multi-user one (which requires Admin privileges). This can be useful if using a corporate-managed machine which does not give the user any freedom.

1. Run the Firefox installer
2. When requested for Admin privileges, decline
3. The installation will proceed locally in the folder `%localappdata%\Mozilla Firefox`

## Migrate/import profiles

1. Go to `%appdata%\Mozilla\Firefox\Profiles` or equivalent
2. Copy to new system
3. Start up new Firefox install, go to `about:profiles` and select the one that you imported
4. Restart browser (and repeat until the default profile is correct)
