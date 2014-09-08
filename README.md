piwik-light
===========

Basic piwik analytics client, with minimal functionality.

For a more complete piwik client, use the standard client from https://piwik.org.

It can send the following information to the piwik server (via GET):

- The URL the user is on
- The referrer
- A random "visitor id" that lasts for only the session, to identify unique
  visits.

And of course, all the standard stuff the browser sends anyway.

It won't send anything if the do not track flag is set in the user's browser.

Usage
=====

Put the piwik-light somewhere on your site. At the bottom of the page put
the following javascript.

```javascript
<script>
    (function () {
        var siteid = 1,
            host = 'yourwebsite.com',
            options = { useHttps: true, sendReferrer: true };
        
        // Loading for the first time
        _piwika = {
            id: siteid,
            host: host,
            options: options 
        };
        // create a new script element
        var script = document.createElement('script');
        script.src = '/javascripts/piwik-light.js';
        script.async = true;

        // insert the script element into the document
        var firstScript = document.getElementsByTagName('script')[0];
            firstScript.parentNode.insertBefore(script, firstScript);
    }());
</script>
```

Note: this script still needs some work I think.

Options
=======

- useHttps (bool): if your piwik is hosted over https (it should)
- sendReferrer (bool): if you want to include the referrer in the info sent
- strictDoNotTrack (bool): if you enable this you probably won't log much. It
  will only send logging information if the do not track flag of the user's
  browser is explicitly set to "yes, track me". If not enabled the library 
  will always track unless the do not track flag is set to "do not track me!"

Background
==========

The piwik client on my blog was too big for my liking, it had a lot of features
I didn't use. Also, it seemed like an interesting small project to learn how to
construct a javascript library.

Any tips if you find something wrong are welcome, obviously!
