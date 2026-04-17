## What?

This is a fork of the original [teams-pwa-link-redirect](https://github.com/frederic-klein/teams-pwa-link-redirect) tool by Frederic Klein adapted to my use case.
It allows you to open links from the Microsoft Teams PWA in your default browser (in my case the Firefox Flatpak) instead of the brower in which the PWA is running.


## Why?

The official Microsoft Teams application for Linux has been deprecated, and the alternatives often ahve issues with Enterprise settings.
The Microsoft Teams PWA is the only officially supported option for Linux users, but it only works well with Chromium-based browsers, and Edge in particular.
Unfortunately, the app does not allow you to choose a different default browser, and it opens links in the same browser in which the PWA is running. 


## How?

This tool introduces two new schemes to handle links outside of the Teams PWA: `tlr` (Teams Link Redirect) and `tlrs` for HTTP and HTTPS links, respectively.
The browser extension modifies all links matching `https?://` to the new schemes, which causes the browser to prompt for approval to open the TLR Handler.
The TLR Handler is defined by the `tlr-handler.desktop` file, which reverts the scheme replacement and opens the links in the default browser using `xdg-open`.


## Installation

1. Clone this repo `git clone git@github.com:leolavaur/teams-pwa-link-redirect.git`
2. Copy the `TLR Handler.desktop` file to `~/.local/share/applications/` and update the `Exec` path if necessary.
3. Install the extension in your browser:
  1. open a chrome-based browser
  2. go to the extensions page (e.g. `edge://extensions/` for Edge)
  3. Enable developer mode
  4. Select "Load unpacked"
  5. Select the cloned repo folder
  6. Reopen the Teams PWA app or `ctrl+F5`
4. associate the schemes with the desktop file:

```bash
xdg-mime default tlr-handler.desktop x-scheme-handler/tlr
xdg-mime default tlr-handler.desktop x-scheme-handler/tlrs
```


## Notification of changes

See the commit history for details on the changes made to the original code.
In summary:
* Changed the naming and updated the scheme accordingly (`ftl` -> `tlr`)
* Updated the handler to use xdg-open
* Updated README.md
* Added the new Teams URL ([https://teams.cloud.microsoft](https://teams.cloud.microsoft))


## Acknoledgments

Thanks to the original contributors for making this helper:
* Frederic Klein ([GitHub](https://github.com/frederic-klein))
* Ryan Cole ([GitHub](https://github.com/ryanc-me))
