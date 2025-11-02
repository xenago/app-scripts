# firefox

Control Mozilla Firefox.

## Prevent sites from automatically being able to save downloads

1. In `about:preferences#general` under `Files and Applications`, select `Always ask you where to save files`
2. Scroll a bit lower down to `Applications` and locate `What should Firefox do with other files?` - set this to  `Ask whether to open or save files`

## `about:config` Overrides

These can be configured by navigating to `about:config` in the address bar and accepting/disable the warning/scare-screen.

There doesn't seem to be an easy way to export or share these settings, sadly. They are defined in `prefs.js` though, so I will eventually look that...

#### Enable a reasonable UI density instead of wasting the screen space

* `browser.compactmode.show` set to `true`
  * Then, right click the browser toolbar UI and select `Customize Toolbar`
  * In the bottom left of the customization menu, select `Density > Compact (not supported)`

#### Disable showing 'suggested sites' in the address bar

This awful setting enables Wikipedia, Facebook, Twitter, YouTube etc. to take up space in the search bar by default.
 
* `browser.urlbar.suggest.topsites` set to `false`

#### Disable ads in the address bar

Yes, [really](https://blog.mozilla.org/en/firefox/better-search-suggestions/)...

> results may be sponsored to support Firefox

* `browser.urlbar.quicksuggest.online.enabled` set to `false`

#### Disable "what's new" page

The page popping up every update is user-hostile and is effectively just an ad to remind users they're on Firefox. The information isn't a useful changelog and users aren't even given a choice to opt out of anything 'new' that is added anyways, so it's pretty much pointless.

These seem hit-or-miss but seem to work most of the time:

* `browser.startup.homepage_override.mstone` set to `ignore`
  * https://kb.mozillazine.org/Browser.startup.homepage_override.mstone
  * Detecting that an update has occured to open a page at startup
  * When a user starts up their browser, this preference is examined. If its value differs from the browser’s current milestone, then the user is redirected to the homepage specified in startup.homepage_override_url and this preference’s value is updated to the current milestone.

* `startup.homepage_override_url` set to `about:blank`
  * https://kb.mozillazine.org/Startup.homepage_override_url
  * When a user starts up their browser after upgrading (i.e., if browser.startup.homepage_override.mstone is different than the last time the browser started), the URL specified in this preference is loaded instead of their homepage

#### Disable AI-ML chatbot

Disable the sidebar in the browser Settings page `about:preferences#browser-layout` first: 

* `browser.ml.chat.enabled` set to `false`

#### Disable AI-ML anti-features

* `browser.tabs.groups.smart.userEnabled` set to `false`
* `browser.tabs.groups.smart` set to `false`
* `browser.ml.linkPreview` set to `false`
* `browser.ml.chat.enabled` set to `false`
* `browser.ml.chat.shortcuts` set to `false`
* `browser.ml.chat.shortcuts.custom` set to `false`
* `browser.ml.chat.sidebar` set to `false`
* `browser.ml.enable` set to `false`

As a sidenote: it is possible to preemptively [block](https://github.com/settings/blocked_users) users on GitHub known to commit ML-generated code, to prevent tainted submissions to your projects.

#### Control tab grouping

A higher delay can be applied to tab groups, since it activates when moving tabs around very easily by default:

* `browser.tabs.dragDrop.createGroup.delayMS` to a large number of milliseconds

Alternatively, tab groups can be disabled entirely:

* `browser.tabs.groups.enabled` set to `false`
* `browser.tabs.groups.smart.enabled` set to `false`

#### Improve clipboard support (useful with e.g. Apache Guacamole)

* `dom.events.asyncClipboard.readText` set to `true`
* `dom.events.testing.asyncClipboard` set to `true`

#### Control tab unloading

This can be useful on low-memory machines and might be useful to disable if there's a lot of RAM in the system. It's unclear if this is a default.

* `browser.tabs.unloadOnLowMemory` set to `true`

#### Restore ability to add custom search engines

This is a particularly ridiculous setting which seems to come and go as one enabled by default.

* `browser.urlbar.update2.engineAliasRefresh` set to `true`

#### Disable OHTTP

They seem to have given up on this for now, but I am keeping an eye out for it.

* `network.trr.use_ohttp` set to `false`
* `network.trr.ohttp.config_uri` set to nothing
* `network.trr.ohttp.relay_uri` set to nothing

#### On 'Developer' version only, disable addon signing

Doesn't apply to most users since this only applies to the rarely-used 'Developer Edition' of Firefox.

Obviously a simple regular user cannot possibly be trusted to run the programs of their own choice golly gee, which means most people are sadly stuck in the walled garden.

* `xpinstall.signatures.required` set to `false`

#### Disable remote extension blocking on '[quarantined](https://support.mozilla.org/kb/quarantined-domains)' domains

This is generally not something one would need to enable, but I don't like digging around for it.

* `extensions.quarantinedDomains.enabled` set to `false`

### The following `about:config` options are placebos

I've seen these around but they don't seem to do anything. I wish they did though, would make automatic updates a lot more usable (read on...)

* `app.update.doorhanger` set to `false`
* `app.update.silent` set to `true`

## `policies.json` override to disable automatic updates

Updates in Firefox have several issues which cannot be normally avoided, such as:

* Automatically enabling new hostile anti-features
* Constant nags to restart the browser
* Inability to configure desired behaviour

As a result, users who want to be treated like competent human beings need to disable the automatic updates entirely, which requires paying attention to security issues and patch notes.

Disabling automatic updates cannot be done using a normal setting, or even `about:config`, ~~because Mozilla does not want their normal users to miss out on whatever nonsense they want to add~~ I mean for safety of course.

Instead, a `policies.json` file [must be created](https://support.mozilla.org/en-US/kb/customizing-firefox-using-policiesjson).

The [`policies.json` file in the repo](policies.json) has been prepared with this config.

* [Download `policies.json`](https://raw.githubusercontent.com/xenago/app-scripts/refs/heads/main/firefox/policies.json) and copy it to one of these `distribution` directories based on the OS (creating it if it does not already exist):
  * Windows - located in the `distribution` folder wherever Firefox is installed
    * System-wide: `C:\Program Files\Mozilla Firefox\distribution`
    * User-only: `%LOCALAPPDATA%\Mozilla Firefox\distribution`
  * Mac: `Firefox.app/Contents/Resources/distribution`
  * Linux
    * `/etc/firefox/policies` or `firefox/distribution`

When automatic updates are disabled, the user can update manually in the `☰ > Help > About Firefox` menu.

## Useful Mozilla-hosted addons

* Block ads: [uBlock Origin](https://addons.mozilla.org/firefox/addon/ublock-origin/)
* Block sponsors embedded in YouTube videos: [SponsorBlock](https://addons.mozilla.org/firefox/addon/sponsorblock/)
* Spoof Chrome to trick badware sites into loading: [Chrome Mask](https://addons.mozilla.org/firefox/addon/chrome-mask/)
* Fix awful Wikipedia UI without logging in: [Classic mode for Wikipedia](https://addons.mozilla.org/firefox/addon/classic-wikipedia/)
* Fix awful Reddit UI without manually going to old subdomain: [Old Reddit Redirect](https://addons.mozilla.org/en-CA/firefox/addon/old-reddit-redirect/)

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

## Identify tabs accessing the network

1. Find IP with increasing data usage in `about:networking#sockets` and copy to clipboard

2. Find corresponding active tab by URL in `about:networking#dns` with Ctrl+F to find domain

## Load unsigned addons

Mozilla is an unethical company that tries to prevent users from running their own code, much like Apple and Google. They gaslight users to try to convince them that this for their own benefit, for 'security', when it is in fact so they can block addons which give the user additional freedom.

Temporary: go to [about:debugging#/runtime/this-firefox](about:debugging#/runtime/this-firefox) to load `manifest.json` from unpacked zip

Permanent: use Firefox Developer Edition with the `xpinstall.signatures.required` tweak.
