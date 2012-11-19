# Audioboo Categories

Boos and channels are categorized into different areas.  You can obtain lists of them via the Categories API.

Get Categories
----
`GET /categories` Returns a list of categories used on Audioboo
Certain categories are only available for boos or for channels, by default this method only returns channel categories. You should filter the result set to only include the type you are interested in by using one of :

* `GET /categories/channels`
* `GET /categories/boos`
* `GET /categories/all`

It is likely that in the future, the default filter on `GET /categories` will change to return all categories rather than just channel-categories.

`GET /categories/all` : 
```json
{
    "body": {
        "categories": [
            {
                "description": "Listen to clips or download one for the road", 
                "id": 6, 
                "title": "Audiobooks", 
                "type": "ChannelCategory"
            }, 
            {
                "description": "Great content from a host of flagship programmes", 
                "id": 1, 
                "title": "BBC", 
                "type": "ChannelCategory"
            }, 
            {
                "description": "From football to Formula 1", 
                "id": 10, 
                "title": "Sport Boos", 
                "type": "AudioClipCategory"
            },
            ...
```

Show category contents
----

`GET /categories/<id>` Returns all channels / boos within the given category.
  
`GET /categories/1` :
```json
{
    "body": {
        "category": {
            "id": 1, 
            "title": "BBC", 
            "type": "ChannelCategory",
            "channels": [
                {
                    "created_at": "2010-06-25T11:00:35Z", 
                    "description": "Welcome to BBC London\u2019s Audioboo page.  \nHere you\u2019ll find highlights and additional material from our newsroom right in the heart of the capital.  Contributions from our reporters and from you.\nGot a story you think we should tell?  \nGet in touch by recording or uploading your story by using the green button or by calling \n0118 413 8272\nBy posting here you agree to your boo being used by BBC London.\nwww.bbc.co.uk/london\n", 
                    "formatted_description": "<p>Welcome to BBC London\u2019s Audioboo page.  </p>\n\n<p>Here you\u2019ll find highlights and additional material from our newsroom right in the heart of the capital.  Contributions from our reporters and from you.</p>\n\n<p>Got a story you think we should tell?  </p>\n\n<p>Get in touch by recording or uploading your story by using the green button or by calling </p>\n\n<h1>0118 413 8272</h1>\n\n<p>By posting here you agree to your boo being used by BBC London.</p>\n\n<p><a href=\"http://www.bbc.co.uk/london\">www.bbc.co.uk/london</a></p>\n", 
                    "id": 49774, 
                    "submission_style": "moderated", 
                    "title": "BBC London's News",
                    "writable": true
                }, 
                {
                    "created_at": "2011-09-03T07:11:16Z", 
                    "description": "Radio 4's morning current affairs programme, broadcast weekdays 6-9, Saturdays 7-9. The comments and views recorded by fans do not represent the views of the BBC.\nJust use the record button below to send us your views. All content will be moderated first.\n", 
                    "formatted_description": "<p>Radio 4&#39;s morning current affairs programme, broadcast weekdays 6-9, Saturdays 7-9. The comments and views recorded by fans do not represent the views of the BBC.</p>\n\n<p>Just use the record button below to send us your views. All content will be moderated first.</p>\n", 
                    "id": 127213, 
                    "submission_style": "moderated", 
                    "title": "BBC Radio 4 Today", 
                    "writable": true
                }
                ...
              
            

```