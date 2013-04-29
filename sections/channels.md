## Channels ##

### Lists of channels ###

 * `GET /channels`
  this call will return a paginated list of channels.

  Finding a channel by matching it's title, adding the querystring below:
    `find[title]=*title*`


### Channel details ###

 * `GET /channels/*channel_id*`
  This will return the details for the channel specified by the *channel_id* parameter.


```json
"body": {
    "channel": {
        "id": 1054469,
        "submission_style": "moderated",
        "writable": true,
        "parent_channel_id": null,
        "created_at": "2013-02-12T16:51:09Z",
        "title": "Audioboo",
        "description": "The Audioboo team here. Bringing you the latest from the office and everywhere else. \nFollow us for updates, offers, competitions and our own special version of community outreach. Get in touch either here, @Audioboo or FB. We love to listen.\nLondon\nhttp://audioboo.fm\n",
        "formatted_description": "<p>The Audioboo team here. Bringing you the latest from the office and everywhere else. \nFollow us for updates, offers, competitions and our own special version of community outreach. Get in touch either here, @Audioboo or FB. We love to listen.\nLondon\n<a href=\"http://audioboo.fm\">http://audioboo.fm</a></p>\n",
        "urls": {
            "logo_image": {
                "original": "http://d15mj6e6qmt1na.cloudfront.net/files/images/0405/4536/audioboo_logo.jpg"
            },
            "banner_image": {
                "original": "http://d15mj6e6qmt1na.cloudfront.net/files/images/0417/0263/audioboo_banner_2.jpg"
            }
        },
        "category": {
            "id": 82,
            "title": "Community",
            "description": ""
        },
        "channel_clips_count": 36,
        "moderation_clips_count": 0
    }
}
```

### Channel audio clips ###

 * `GET /channels/*channel_id*/audio_clips`
  This will return the audio_clips for the channel specified by the *channel_id* parameter.