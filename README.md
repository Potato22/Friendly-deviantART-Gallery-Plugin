Friendly deviantART-Gallery-Plugin
=========================

HEAVILY MODIFIED BY Potto
DOES NOT INCLUDE [simpleslider](https://github.com/jamesl1001/simpleslider)

Embed your deviantART gallery with this Javascript plugin.

This plugin contains two of [Jamesl1001](https://github.com/jamesl1001/deviantART-Gallery-Plugin)'s projects: 
[deviantART-API](https://github.com/jamesl1001/deviantART-API)
[deviantArt-Gallery-Plugin](https://github.com/jamesl1001/deviantART-Gallery-Plugin)

Usage
-----

1 - Link to `deviantART-gallery.min.css` in the `<head>` tag:

```html
<link rel="stylesheet" type="text/css" href="deviantART-gallery.min.css"/>
```

2 - Add the scripts before the closing `</body>` tag:

```html
    <script src="deviantART-gallery-plugin.js"></script>
    <script>
        //for debug only, can be skipped.
        getDeviations("https://backend.deviantart.com/rss.xml?q=gallery:"+USERNAME+"/"+GalleryId, null, 0);

        function processDeviations(deviations) {
            for (var i = 0, l = deviations.length; i < l; i++)
            //THIS WILL SPAM YOUR CONSOLE LOG, CONVENIENT FOR DEBUGGING
            /*
            {
                console.log(deviations[i].title);
                console.log(deviations[i].link);
                console.log(deviations[i].image);
            }
            */
            console.log('[DAGP] UPDATED')
        }
    </script>
```
note: for further debugging purposes, you can uncomment the commented part of the script. If not you can remove it completely.  
To disable all debugging (from the script file), use the one without '**debug**' on its file name or the **minified** version.



3 - Add the following element where the gallery is to be positioned:

```html
<div class="gridbox" id="daImg">
```
You can customize **directly** what the script will inject into, make sure it's an **ID** name instead of class.
The gridbox is just for demonstration purposes, feel free to customize it and use any other methods.

Additional info
---------------
To enter your username and gallery ID, you can edit the const string directly inside the script file.  
```js
const USERNAME = "YOURNAME"
const GalleryId = "GALLERYID"
```
Gallery ID's can be found by looking at your gallery url
`https://www.deviantart.com/potato2292/gallery/`**`78916640`**`/pottofolio`  

You can directly change what element the script injects into DOM by editing the template inside the script file.
```js
function deviantARTGalleryPlugin(e, t, n) {
    var s = [];
    ! function () {
        console.log("[DAGP] fetching user:", e, "folder:", t, "");
        var a = "https://backend.deviantart.com/rss.xml?q=gallery:"+USERNAME+"/"+GalleryId+":" + e + "/" + t;
        window.callback = function (e) {
            for (var t = e.items, a = 0, i = t.length; a < i; a++) {
                var l = {};
                l.title = t[a].title, l.image = t[a].enclosure.link, s.push(l)
            }
            for (var d = "", a = 0, i = s.length; a < i; a++) d += 
            //Below is the element that the script will inject into DOM.
            //Element will repeat with the amount of images requested/limited to.
            // ### Feel free to customize it. ###
            '<img style="position: relative; max-width:100%; overflow: hidden;" src="' + s[a].image + '"/>';

            document.getElementById(TARGET).innerHTML = d, console.log("[DAGP] images fetched.\n", e.feed.title, "\n", e.status, "\n\n Plugins by jamesl1001\nhttps://github.com/jamesl1001/deviantART-Gallery-Plugin\nhttps://github.com/jamesl1001/deviantART-API\n\nThis version was heavily modified by Potto.");
            const event = new Event("finish");
            document.getElementById(TARGET).dispatchEvent(event)
        };
        var i = document.createElement("script");
        i.src = "https://api.rss2json.com/v1/api.json?callback=callback&rss_url=" + escape(a), document.body.appendChild(i)
    }()
}
```

Quick QNA
---
**Is there anyway to incrase or change the amount of images to display?**  
_As of now, I couldn't find way to do just that. Sorry!_
