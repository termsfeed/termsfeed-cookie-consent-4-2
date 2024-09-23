# TermsFeed Free Cookie Consent, version 4.2

Free Cookie Consent is a free cookies management solution by [TermsFeed](https://www.termsfeed.com) that you can integrate on your website that helps you comply with the EU Cookies Directive and GDPR.

The Free Cookie Consent 4.2 can be used to integrate Google Consent Mode V2, see [Example > Google Consent Mode V2](#google-consent-mode-v2)

# Installation

## Hosted by TermsFeed

1. Load the Cookie Consent from TermsFeed domain.

        <script type="text/javascript" src="//www.termsfeed.com/public/cookie-consent/4.2.0/cookie-consent.js" charset="UTF-8"></script>

2. Append the config code.
3. Add the code after the `<body>` tag or before the `</body>` tag on your web pages. Example:

        <script type="text/javascript" src="//www.termsfeed.com/public/cookie-consent/4.2.0/cookie-consent.js"></script>
        <script type="text/javascript">
            document.addEventListener('DOMContentLoaded', function () {
                cookieconsent.run({
                    "notice_banner_type": "headline",
                    "website_privacy_policy_url": "http://www.termsfeed.com/",
                    "consent_type": "express",
                    "palette": "light",
                    "website_name": "TermsFeed Cookie Consent",
                    "language": "en",
                    "open_preferences_center_selector": "#changePreferences",
                    "preferences_center_close_button_hide": false,
                    "page_load_consent_levels": ["strictly-necessary"]
                });
            });
        </script>

## Self-host

1. Copy the `cookie-consent.js` from `dist/` folder.
2. Append the config code.
3. Add the code after the `<body>` tag or before the `</body>` tag on your web pages. Example:

        <script type="text/javascript" src="cookie-consent.js"></script>
        <script type="text/javascript">
            document.addEventListener('DOMContentLoaded', function () {
                cookieconsent.run({
                    "notice_banner_type": "headline",
                    "website_privacy_policy_url": "http://www.termsfeed.com/",
                    "consent_type": "express",
                    "palette": "light",
                    "website_name": "TermsFeed Cookie Consent",
                    "language": "en",
                    "open_preferences_center_selector": "#changePreferences",
                    "preferences_center_close_button_hide": false,
                    "page_load_consent_levels": ["strictly-necessary"]
                });
            });
        </script>

# Usage

In order for the Cookie Consent tool to run correctly, you need to "tag" your JS scripts:

1. Change `type="text/javascript"` to `type="text/plain"`. If `type="text/javascript"` is not available, add `type="text/plain"`.
2. On the same `<script>`, add in the corresponding cookie level: `data-cookie-consent="functionality"`.

Here's an example:

    <!-- Login Cookies -->
    <script type="text/plain" data-cookie-consent="strictly-necessary" src="/js/login-session.js"></script>

    <!-- Google Analytics -->
    <script type="text/plain" data-cookie-consent="tracking">
    (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
    (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
    m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
    })(window,document,'script','//www.google-analytics.com/analytics.js','ga');
    ga('create', GOOGLE_PROPERTY_ID_GOES_HERE, 'auto');
    ga('send', 'pageview');
    </script>

# Example

The below example includes the install + config code, the button to open Preferences Center and an example of JS script tagged.

    <!-- Cookie Consent by TermsFeed https://www.TermsFeed.com -->
     <script type="text/javascript" src="//www.termsfeed.com/public/cookie-consent/4.2.0/cookie-consent.js" charset="UTF-8"></script>
    <script type="text/javascript" charset="UTF-8">
        document.addEventListener('DOMContentLoaded', function () {
            cookieconsent.run({
                    "notice_banner_type": "headline",
                    "website_privacy_policy_url": "http://www.termsfeed.com/",
                    "consent_type": "express",
                    "palette": "light",
                    "website_name": "TermsFeed Cookie Consent",
                    "language": "en",
                    "open_preferences_center_selector": "#changePreferences",
                    "preferences_center_close_button_hide": false,
                    "page_load_consent_levels": ["strictly-necessary"]
            });
        });
    </script>
    <noscript>Free cookie consent management tool by <a href="https://www.termsfeed.com/">TermsFeed</a></noscript>
    <!-- End Cookie Consent by TermsFeed https://www.TermsFeed.com -->

    <!-- Below is the link that users can use to open Preferences Center to change their preferences. Do not modify the ID parameter. Place it where appropriate, style it as needed. -->
    <button id="changePreferences">Change preferences</button>

    <!-- Google Analytics -->
    <script type="text/plain" data-cookie-consent="tracking">
    (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
    (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
    m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
    })(window,document,'script','//www.google-analytics.com/analytics.js','ga');
    ga('create', GOOGLE_PROPERTY_ID_GOES_HERE, 'auto');
    ga('send', 'pageview');
    </script>

## Google Consent Mode V2

Create the `gtag` function with the default consent states as denied. Then load the Google Analytics script. And then, using the callbacks functionality of the TermsFeed Free Cookie Consent, update the consent states based on user acceptance.

1. First, set the default consent states to `denied`.

        <script>
        window.dataLayer = window.dataLayer || [];
        function gtag(){
                dataLayer.push(arguments);
        }
        gtag('consent', 'default', {
                'ad_storage': 'denied',
                'ad_user_data': 'denied',
                'ad_personalization': 'denied',
                'analytics_storage': 'denied'
        });
        </script>

2. Load Google Analytics on your page without tagging it to a specific category. With the default consent states as denied, Google Analytics will adjust its behavior accordingly in order to preserve analytics measurement.

        <script async src="https://www.googletagmanager.com/gtag/js?id=TAG_ID"></script>
        <script>
        	window.dataLayer = window.dataLayer || [];
        	function gtag(){dataLayer.push(arguments);}
        
        	gtag('js', new Date());
        	gtag('config', 'TAG_ID');
        </script>

3. Update your Cookie Consent config code to include a new parameter called `callbacks` that updates the consent states based on user consent.

        "callbacks": {
                  "scripts_specific_loaded": (level) => {
                            switch(level) {
                                      case 'tracking':
                                                gtag('consent', 'update', {
                                                          'analytics_storage': 'granted'
                                                });
                                                break;
                                      case 'targeting':
                                                gtag('consent', 'update', {
                                                          'ad_storage': 'granted',
                                                          'ad_user_data': 'granted',
                                                          'ad_personalization': 'granted'
                                                });
                                                break;
                            }
                  }
        },
        "callbacks_force": true

4. The final code should look like this:

        <!-- gtag function with denied consent as default -->
        <script>
        window.dataLayer = window.dataLayer || [];
        function gtag(){
        	dataLayer.push(arguments);
        }
        gtag('consent', 'default', {
                'ad_storage': 'denied',
                'ad_user_data': 'denied',
                'ad_personalization': 'denied',
        	'analytics_storage': 'denied'
        });
        </script>
        <!-- End of gtag function with denied consent as default -->
        
        <!-- Load GTM tag script -->
        <script async src="https://www.googletagmanager.com/gtag/js?id=TAG_ID"></script>
        <script>
        	window.dataLayer = window.dataLayer || [];
        	function gtag(){dataLayer.push(arguments);}
        
        	gtag('js', new Date());
        	gtag('config', 'TAG_ID');
        </script>
        <!-- End of Load GTM tag script -->
        
        <!-- Cookie Consent by TermsFeed https://www.TermsFeed.com -->
        <script type="text/javascript" src="//www.termsfeed.com/public/cookie-consent/4.2.0/cookie-consent.js" charset="UTF-8"></script>
        <script type="text/javascript" charset="UTF-8">
        document.addEventListener('DOMContentLoaded', function () {
        	cookieconsent.run({
        		"notice_banner_type": "simple",
        		"consent_type": "express",
        		"palette": "dark",
        		"language": "en",
        		"page_load_consent_levels": ["strictly-necessary"],
        		"notice_banner_reject_button_hide": false,
        		"preferences_center_close_button_hide": false,
        		"page_refresh_confirmation_buttons": false,
        		"website_privacy_policy_url": "https://www.termsfeed.com/",
        		"callbacks": {
        			"scripts_specific_loaded": (level) => {
        				switch (level) {
        					case 'tracking':
        						gtag('consent', 'update', {
        							'analytics_storage': 'granted'
        						});
        						break;
        					case 'targeting':
        						gtag('consent', 'update', {
        							'ad_storage': 'granted',
        							'ad_user_data': 'granted',
        							'ad_personalization': 'granted'
        						});
        						break;
        				}
        			}
        		},
        		"callbacks_force": true
        	});
        });
        </script>
        
        <noscript>Free cookie consent management tool by <a href="https://www.termsfeed.com/">TermsFeed</a></noscript>
        <!-- End Cookie Consent by TermsFeed https://www.TermsFeed.com -->


# Credits Link

The Credits Link must be kept in the HTML source code (see Example above) and inside the Preferences Center.
    
# Design

You can apply your own style for the Cookie Consent by writing your own CSS to overwrite the CSS of Cookie Consent.

Use Developer Tools > Inspect Element to identify the element you want to customize and style differently. Then write your own CSS rules to overwrite the style of the element. For example, if you'd like to make the title of the notice banner red then:

    .termsfeed-com---nb .cc-nb-title {
      color: red !important;
    }

# Methods

The following methods are available for the Cookie Consent:

| Name | Description |
|------|-------------|
| `cookieconsent.run();` | The `run()` method initiates the Cookie Consent. It accepts the configuration options (see below). |
| `cookieconsent.openPreferencesCenter();` | The `openPreferencesCenter()` can be used to open the Preferences Center if the classic method (ie. naming the ID of the button/link in the configuration options) is not available. For example, in single-page applications (SPAs). |

# Configuration Options

The following configurations are available for the Cookie Consent that can be used with the `cookieconsent.run()` method:

| Name | Type | Default | Values | Description |
|------|------|---------|--------|-------------|
| `consent_type` | String | `express` | `express`, `implied` | Type of consent to apply. `implied` will automatically load all tagged JS scripts on page load without waiting for consent. `express` will not load any tagged JS scripts (except strictly necessary) until the user clicks "I Agree". |
| `notice_banner_type` | String | `headline` | `simple`, `headline`, `interstitial`, `standalone` | Type of notice banner design to apply. |
| `palette` | String | `light` | `light`, `dark` | Color palette to apply. |
| `language` | String | `en` | See `i18n/` folder | Language for the text inside the notice banner and Preferences Center. |
| `open_preferences_center_selector` | String | `#changePreferences` | | The ID of the button/link to open the Preferences Center. |
| `website_name` | String | | | The website name to appear in Preferences Center. |
| `website_privacy_policy_url` | String | | | Sets the URL to the Cookies Policy. It appears in the Preferences Center > More Information tab. |
| `website_impressum_url` | String | | | Sets the URL to the Impressum. It appears in the Preferences Center > More Information tab. |
| `notice_banner_purposes_levels` | Array | `["strictly-necessary", "functionality", "tracking", "targeting"]` | `["strictly-necessary", "functionality", "tracking", "targeting"]` | Categories of purposes mentioned in the notice banner text and corresponding tabs in Preferences Center. |
| `notice_banner_insert_legal_urls` | Boolean | `false` | `true`, `false` | Shows the URLs to the Privacy Policy and Impressum in notice banner text (1st layer). |
| `notice_banner_append` |  String | `afterbegin` | `afterbegin`, `beforeend` | Controls where the Cookie Consent injection code is added (afterbegin or beforeend). |
| `preferences_center_close_button_hide` |  Boolean | `false` | `true`, `false` | Shows or hides the "Close" / "X" button in Preferences Center. |
| `page_load_consent_levels` |  Array |  | `["strictly-necessary", "functionality", "tracking", "targeting"]` | Determines the categories of tagged scripts to loaded on page load. The `implied` consent mode should contain all categories while the `express` consent mode should contain only the `strictly-necessary`. |
| `page_refresh_confirmation_buttons` |  Boolean | `false` | `true`, `false` | Refreshes the page upon user's action (i.e. clicking "I Agree" or "I Decline"). |
| `user_consent_token` |  String |  |  | Store your own user consent token (to be used for consent log functionality). |
| `cookie_domain` |  String |  |  | Sets the domain in the stored cookies (to be used for sub-domains). |
| `cookie_secure` |  Boolean | `false` | `true`, `false` | Sets the secure flag for the stored cookies. |
| `callbacks` |   |  |  | See Callbacks below. |
| `callbacks_force` |  Boolean | `false` | `true`, `false` | Fires callbacks regardless if tagged scripts are available on page or not. |
| `demo` |  Boolean | `false` | `true`, `false` | Demo mode will not save any cookies. |
| `debug` |  Boolean | `false` | `true`, `false` | Debug mode will output Console message. |

## Callbacks

You can use callbacks to integrate additional logic with Cookie Consent.

Supported events are:

- `i_agree_button_clicked` (when user has clicked on "I Agree" button)
- `i_decline_button_clicked` (when user has clicked on "I Decline" button)
- `change_my_preferences_button_clicked` (when user has clicked on "Change Preferences" button)
- `scripts_specific_loaded (when scripts` from a specific category have loaded)
- `user_consent_saved` (when user consent preference is updated)

Example of callbacks code:

        "callbacks": {
            "notice_banner_loaded": () => {
                let timestamp = currentDate.toISOString();
                console.log("[" + timestamp + "] >>>>>>> called notice_banner_loaded callback from dist/index.html");
            },
            "i_agree_button_clicked": () => {
                let timestamp = currentDate.toISOString();
                console.log("[" + timestamp + "] >>>>>>> called I Agree button callback from dist/index.html");
            },
            "i_decline_button_clicked": () => {
                let timestamp = currentDate.toISOString();
                console.log("[" + timestamp + "] >>>>>>> called I Decline button callback from dist/index.html");
            },
            "change_my_preferences_button_clicked": () => {
                let timestamp = currentDate.toISOString();
                console.log("[" + timestamp + "] >>>>>>> called Change My Preferences button callback from dist/index.html");
            },
            "scripts_all_loaded": () => {
                let timestamp = currentDate.toISOString();
              console.log("[" + timestamp + "] >>>>>>> called Scripts All loaded callback from dist/index.html");
            },
            "scripts_specific_loaded": (level) => {
                let timestamp = currentDate.toISOString();
        
                // Levels
                switch(level) {
                    case 'strictly-necessary':
                        console.log("[" + timestamp + "] >>>>>>> called Scripts " + level + " loaded callback from dist/index.html");
                        break;
                    case 'functionality':
                        console.log("[" + timestamp + "] >>>>>>> called Scripts " + level + " loaded callback from dist/index.html");
                        break;
                    case 'tracking':
                        console.log("[" + timestamp + "] >>>>>>> called Scripts " + level + " loaded callback from dist/index.html");
                        break;
                    case 'targeting':
                        console.log("[" + timestamp + "] >>>>>>> called Scripts " + level + " loaded callback from dist/index.html");
                        break;
                }
            }
        }

You can use function names instead of code to fire your own functions:

        "callbacks": {
            "scripts_specific_loaded": "my_function_for_scripts_specific_loaded"
        }

Callbacks are fired only if tagged scripts are found on page. Otherwise, to fire callbacks when consent category is accepted without any tagged scripts on page, add `callbacks_force` as `true`.

# Disclaimer

Legal information is not legal advice, [read the disclaimer](https://www.termsfeed.com/legal/disclaimer/).

The provided tool is informational purposes only and do not constitute legal advice.

The information provided here is not legal advice, does not constitute a lawyer referral service, and no attorney-client or confidential relationship is or will be formed by use of the tool.

# License

Shield: [![CC BY-NC-SA 4.0][cc-by-nc-sa-shield]][cc-by-nc-sa]

This work is licensed under a
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa].

[![CC BY-NC-SA 4.0][cc-by-nc-sa-image]][cc-by-nc-sa]

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/
[cc-by-nc-sa-image]: https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png
[cc-by-nc-sa-shield]: https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg
