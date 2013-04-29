# API Reference #

## Things to know / remember ##

The API is REST-based.   All requests follow a standard format, see the [api introduction](https://github.com/audioboo/api/blob/master/sections/request_formats.md) for an overview of how to perform these requests.

All parts of a URL in bold are parameters that should be replaced before making calls!

Any `/account/...` urls will act on the user corresponding to the OAuth access token provided. They will return an unauthorized response if OAuth authentication hasn't been performed.

----

The different API endpoints are broken up by section :

### [Boos / AudioClips](https://github.com/audioboo/api/blob/master/sections/audio_clips.md)
### [Followers](https://github.com/audioboo/api/blob/master/sections/followers.md)
### [Messages](https://github.com/audioboo/api/blob/master/sections/messages.md)
### [Users](https://github.com/audioboo/api/blob/master/sections/users.md)
### [Playlists](https://github.com/audioboo/api/blob/master/sections/playlists.md)
### [Favourites](https://github.com/audioboo/api/blob/master/sections/favourites.md)
### [Channels](https://github.com/audioboo/api/blob/master/sections/channels.md)
### [Uploading Chunked (Partial) Files](https://github.com/audioboo/api/blob/master/sections/chunked_attachments.md)

----


### Blocking ###
Some users may be blocked from messaging or following others.

If you GET the details of an individual user, there is a `messaging_enabled` flag indicating whether that user can be messaged, and likewise for the `following_enabled` flag

Each message in the inbox contains a `user[messaging_enabled]` flag showing if that message can be replied to.



### Image Formats ###
Only JPEG and PNG image formats are tested and known to work at the point.

### Audio Formats ###
We will attempt to transcode any audio file that you throw at us.  We explicitly support FLAC, MP3, and AIFF/WAV.

### File Uploads ###

Files should be sent using HTTP multipart encoding.  You must include a 'filename' parameter in the Content-Disposition multipart header, to ensure that our webserver processes it as a file.  If you're authenticating via OAuth, be sure to use the [Body Hash extension](http://oauth.googlecode.com/svn/spec/ext/body_hash/1.0/oauth-bodyhash.html).