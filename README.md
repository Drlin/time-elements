# &lt;time&gt; element extensions

Formats a timestamp as a localized string or as relative text that auto-updates in the user's browser.

This allows the server to cache HTML fragments containing dates and lets the browser choose how to localize the displayed time according to the user's preferences. For example, the server may have cached the following generated markup:

```html
<local-time datetime="2014-04-01T16:30:00-08:00">
  April 1, 2014 4:30pm
</local-time>
```

Every visitor is served the same markup from the server's cache. When it reaches the browser, the custom `local-time` JavaScript localizes the element's text into the local timezone and formatting.

```html
<local-time datetime="2014-04-01T16:30:00-08:00">
  1 Apr 2014 21:30
</local-time>
```

Dates are displayed before months, and a 24-hour clock is used, according to the user's browser settings.

If the browser's JavaScript is disabled, the default text served in the cached markup is still displayed.

## Installation

Available on [Bower](http://bower.io) as **time-elements**.

```
$ bower install time-elements
```

This component is built on the upcoming [Web Component](http://webcomponents.org/) stack. Specifically, it requires a feature called [Custom Elements](http://www.html5rocks.com/en/tutorials/webcomponents/customelements/).

You'll need to use a polyfill to get this feature today. Either the [Polymer](http://www.polymer-project.org/) or [X-Tag](http://www.x-tags.org/) frameworks supply a polyfill, or you can install the standalone [CustomElements](https://github.com/webcomponents/webcomponentsjs) polyfill.

``` html
<script src="https://cdnjs.cloudflare.com/ajax/libs/webcomponentsjs/0.5.4/CustomElements.min.js"></script>
```

## Usage

This component provides three custom subtypes of the standard HTML `<time>` element. All custom time elements MUST have a `datetime` attribute set to an ISO 8601 formatted timestamp.

### relative-time

A relative time-ago-in-words description can be generated by using the `relative-time` element extension.

Add a `<relative-time>` element to your markup. Provide a default formatted date as the element's text content (e.g. April 1, 2014).

``` html
<relative-time datetime="2014-04-01T16:30:00-08:00">
  April 1, 2014
</relative-time>
```

Depending on how far in the future this is being viewed, the element's text will be replaced with one of the following formats:

- 6 years from now
- 20 days from now
- 4 hours from now
- 7 minutes from now
- just now
- 30 seconds ago
- a minute ago
- 30 minutes ago
- an hour ago
- 20 hours ago
- a day ago
- 20 days ago
- on Apr 1, 2014

So, a relative date phrase is used for up to a month and then the actual date is shown.

### time-until

You can use `time-until` to always display a relative date that's in the future. It operates much like `<relative-time>`, except in the reverse, with past events shown as `just now` and future events always showing as relative:

- 10 years from now
- 20 days from now
- 6 hours from now
- 20 minutes from now
- 30 seconds from now
- just now

Add a `<time-until>` element to your markup. Provide a default formatted date as the element's text content (e.g. April 1, 2024).

``` html
<time-until datetime="2024-04-01T16:30:00-08:00">
  April 1, 2024
</time-until>
```

### time-ago

An *always* relative time-ago-in-words description can be generated by using the `time-ago` element extension. This is similar to the `relative-time` extension. However, this will never switch to displaying the date. It strictly shows relative date phrases, even after a month has passed.

``` html
<time-ago datetime="2012-04-01T16:30:00-08:00">
  April 1, 2014
</time-ago>
```

For example, if this markup is viewed two years in the future, the element's text will read `2 years ago`.

#### Micro format

The optional `format="micro"` attribute shortens the descriptions to 1m, 1h, 1d, 1y.

``` html
<time-ago datetime="2012-04-01T16:30:00-08:00" format="micro">
  April 1, 2014
</time-ago>
```

### local-time

This custom time extension is useful for formatting a date and time in the user's preferred locale format.

``` html
<local-time datetime="2014-04-01T16:30:00-08:00"
    month="short"
    day="numeric"
    year="numeric"
    hour="numeric"
    minute="numeric">
  April 1, 2014 4:30PM PDT
</local-time>
```

When this markup is viewed in a CDT timezone, it will show `Apr 1, 2014 6:30PM`. If it's viewed in a browser with European date preferences, it will read `1 Apr 2014 18:30`.

### Options

Attribute      | Options                        | Description
---            | ---                            | ---
`datetime`     | ISO 8601 date                  | Required date of element `2014-06-01T13:05:07Z`
`year`         | 2-digit, numeric               | Format year as `14` or `2014`
`month`        | short, long                    | Format month as `Jun` or `June`
`day`          | 2-digit, numeric               | Format day as `01` or `1`
`weekday`      | short, long                    | Format weekday as `Sun` or `Sunday`
`hour`         | 2-digit, numeric               | Format hour as `01` or `1`
`minute`       | 2-digit, numeric               | Format minute as `05` or `5`
`second`       | 2-digit, numeric               | Format second as `07` or `7`

## Browser Support

![Chrome](https://raw.github.com/alrra/browser-logos/master/chrome/chrome_48x48.png) | ![Firefox](https://raw.github.com/alrra/browser-logos/master/firefox/firefox_48x48.png) | ![IE](https://raw.github.com/alrra/browser-logos/master/internet-explorer/internet-explorer_48x48.png) | ![Opera](https://raw.github.com/alrra/browser-logos/master/opera/opera_48x48.png) | ![Safari](https://raw.github.com/alrra/browser-logos/master/safari/safari_48x48.png)
--- | --- | --- | --- | --- |
Latest ✔ | Latest ✔ | 9+ ✔ | Latest ✔ | 6.1+ ✔ |

## See Also

Most of this implementation is based on Basecamp's [local_time](https://github.com/basecamp/local_time) component. Thanks to @javan for open sourcing that work and allowing for others to build on top of it.

@rmm5t's [jquery-timeago](https://github.com/rmm5t/jquery-timeago) is one of the old time-ago-in-words JS plugins.
