# API Reference #

## Things to know / remember ##
<font color='red'> This is a work in progress and meant as a hint to start playing with the API. If you can guess what an API does then by all means give it a go!</font>

The API is REST-based.   All requests follow a standard format, see the [RequestFormat api introduction] for an overview of how to perform these requests.

All parts of a URL in bold are parameters that should be replaced before making calls!

Any `/account/...` urls will act on the user corresponding to the OAuth access token provided. They will return an unauthorized response if OAuth authentication hasn't been performed.

----

## Audio Clips ##

### All audio clips ###

These return [paginated] responses.

 * GET /audio_clips.*format*
  returns all boos in chronological order (most recent first)
 * GET /audio_clips.*format*?find`[`query`]`=*query*
  searches for boos matching the *query* search term.
  returns all boos in chronological order (most recent first)
 * GET /audio_clips/featured.*format*
  returns the editorially "featured" boos as appear on the web-site
 * GET /audio_clips/popular.*format*
  returns the most popular audio clips ordered by recent listens

### Tagged audio clips ###
This call will return a [paginated] response.

 * GET /tag/*tag*/audio_clips.*format*
  returns all the audio clips tagged with the specified tag. The tag in the URL should be [TagNormalisation normalised].
  
###User's audio clips###
These calls will return [paginated] responses.

 * GET /users/*user_id*/audio_clips.*format*
  returns the audio clips uploaded by the user specified by *user_id*.

 * GET /audio_clips.*format*?username=*username*
  returns the audio clips uploaded by *username*.  If known, using the user's id is preferred, since it's guaranteed to never change.

 * GET /account/audio_clips.*format* 
  returns the audio_clips uploaded by the user linked to the OAuth access token used.

### User's followed clips ###
These calls will return [paginated] responses.

 * GET /users/*user_id*/audio_clips/followed.*format*
  returns the audio clips uploaded by users followed by the user specified by *user_id*.

 * GET /account/audio_clips/followed.*format*
  returns the audio clips uploaded by users followed by the user linked to the OAuth access token used.

### Clips by location ###

#### Filtering for clips with location ####
There is a feed of boos restricted only to those with a public location, which may be useful for generating maps of boos, etc.
This can be accessed using a call to the URL:

 * GET /audio_clips/located.*format*

<font color="red">At the moment it doesn't follow the same rules regarding context (i.e. /users/12/audio_clips/located.json won't return user 12's located clips - this is a major FIXME for me...)</font>

#### Search by distance from point ####
If you want to get a list of boos increasing near a specific long/lat point you can call this:

 * GET /audio_clips/located.*format*`?`find`[`latitude`]`=*latitude*`&`find`[`longitude`]`=*longitude*

The results will be ordered by a combination of how recent they are and how far away from the point they are, so something 20m away done 2 days ago could be after something 100m away done 1 hour ago. There isn't currently a way to manipulate this behaviour.

Comments welcomed/appreciated but unfortunately not enough time to act on them in the near future.

#### Search for boos "nearby" ####
You can search for clips nearby another clip:

 * GET /audio_clips/*clip_id*/nearby.*format*

Which will return clips in the same order as clips returned from a long/lat point. For this and the clips from point call you'll also get a "bearing" and "distance" tag in the returned XML for each result which will tell you the bearing and distance of each result from the query location, using the haversine approximation. Don't know if that is useful, but it's there!

#### Clips within a bounding box ####
You can request all the clips that fall within an arbitrary bounding box.

 * GET /audio_clips/located.*format*`?`BBOX=*west*,*south*,*east*,*north*

Pagination rules apply, so it's possible to retrieve *all* clips inside the box...

#### Google Earth KML Feed ####

Just "for fun" there is a KML generator which you can plug in to google earth. Absolutely unsupported and will potentially break in the future :-)

Add a "network link" in google earth to this url

 * http://api.audioboo.fm/audio_clips/located.kml

And you'll get the push-pins / audioboo icons on the map. You can even specify the view based refresh and google earth will automatically load clips from the viewport as you move around the map.

If you use:

 * http://api.audioboo.fm/audio_clips/located.kml?tour=true

Then it will produce a KML with a tour of the most recent clips.

### Audio clip details ###

 * GET /audio_clips/*audio_clip_id*.*format*
  returns the details of the audio clip specified by *audio_clip_id*.

 * GET /audio_clips/*audio_clip_id*.mp3
  this will respond with a browser re-direct to the mp3 audio data for the audio clip specified by *audio_clip_id*

### Posting audio clips ###

POST /account/audio_clips.*format*

this will post an audio clip into the recent clips of the user linked to the OAuth access token used.

To post to a channel, you can use 

POST /channels/*channel_id*/audio_clips.*format*

which will post an audio clip to the specified channel.

The same parameters are used for either endpoint: 


 * `audio_clip[uploaded_data]` (required)
  The uploaded audio data as a multipart file, see [ReferenceIndex#Audio_Formats] and [ReferenceIndex#File_Uploads].

 * `audio_clip[uuid]` (recommended)
  A [http://en.wikipedia.org/wiki/Universally_unique_identifier universally unique identifier], to aid the server in duplicate-detection.  The uuid must not contain spaces or a newline characters.

 * `audio_clip[uploaded_image]`
  The uploaded image data as a multipart file, see see [ReferenceIndex#Image_Formats] and [ReferenceIndex#File_Uploads].

 * `audio_clip[title]`
  The title for the audio clip.

 * `audio_clip[recorded_at]` 
  The time that the clip was recorded, in "YYYY-MM-DD HH:MM:SS ±HHMM" format.

 * `audio_clip[tag_list]`
  The tags to associate with the audio clip. These should be comma separated, and use quotes if the tag itself contains a comma. 

 * `audio_clip[public_location]`
  Boolean value indicating if location should be public on the website. Use strings 'true' or 'false'.

If public_location is true, the server expects these values to also be completed:
 * `audio_clip[location_latitude]`
  The latitude value of the location, encoded as a string representation of a decimal number between -90.0 (south) to +90.0 (north).

 * `audio_clip[location_longitude]`
  The longitude value of the location, encoded as a string representation of a decimal number between -180.0 (westwards) and 180.0 (eastwards).

 * `audio_clip[location_accuracy]`
  The accuracy of the reading, in meters - omit this value if it's not available.

### Image Formats ###
Only JPEG and PNG image formats are tested and known to work at the point.

### Audio Formats ###
We will attempt to transcode any audio file that you throw at us.  We explicitly support FLAC, MP3, and AIFF/WAV.

### File Uploads ###

Files should be sent using HTTP multipart encoding.  You must include a 'filename' parameter in the Content-Disposition multipart header, to ensure that our webserver processes it as a file.  If you're authenticating via OAuth, be sure to use the [http://oauth.googlecode.com/svn/spec/ext/body_hash/1.0/oauth-bodyhash.html Body Hash extension].

### Updating audio clips ###

You can update audio clips by sending a PUT request to the boo's location : 

PUT /audio_clips/*audio_clip_id*.*format*

It accepts the same parameters as those shown in the creation method.

### Deleting audio clips ###

You can mark audio clips for deletion by sending a DELETE request to the boo's location :

DELETE /audio_clips/*audio_clip_id*.*format*

----

## Users ##

### Lists of Users ###

 * GET /users.*format*
  this call requires exactly one of two parameters to find a specific user. The behavior if both parameters are supplied is undefined.

    `find[username]=*username*`

    will return _at most_ one user who has the specified user exactly. This is the recommended way to find an id for a named user.

   `find[query]=*query*`

   will perform a more flexible search for the query against the users on the system. It can return multiple users that match the query and you can use the `*` as a wildcard


### User details ###

 * GET /users/*user_id*.*format*
  This will return the details for the user specified by the *user_id* parameter.

 * GET /account.*format*
  This will return the details of the user linked to the OAuth access token.

## Listing followers / following users ##
Just to clarify:

Followers = users who have chosen to follow a user

Followings = users who a specific user is following

 * GET /users/*user_id*/followings.*format*
 * GET /account/followings.*format*

 * GET /users/*user_id*/followers.*format*
 * GET /account/followers.*format*

You can specify a `find[user_id]` parameter to limit the results to a particular set of users. To, for example, find out if stephen fry is following you, you'd call:

GET /account/followers.*format*?find`[`user_id`]`=11

You can supply multiple, comma-separated id's to restrict to a series of users, to find if any of the Audioboo team are following you, try:

GET /account/followers.*format*?find`[`user_id`]`=12,17,5,30,16

### Creating and Deleting followings ###

 * POST /account/followings.*format*
 * DELETE /account/followings.*format*

  Both of these calls require a single parameter `following_user_id` which is the id of the user to follow or un-follow.

----

## Messaging ##

All of these calls require an authenticated user.

### Inbox ###

The messages in the user's inbox. [Paginated] and in chronological order (most recent first)
 * GET /account/inbox*.format*

### Message details ###

 * GET /account/messages/*message_id*.*format*
 returns the details of the message specified by *message_id*.

### Post message ###
This will send a message to another user (from the authenticated user).

 * POST /account/outbox(.:format)

The following parameters are identical to posting an audio clip:

 * `message[uploaded_data]` (required)
 * `message[uuid]` (recommended)
 * `message[uploaded_image]`
 * `message[title]`
 * `message[recorded_at]`
 * `message[location_latitude]`
 * `message[location_longitude]`
 * `message[location_accuracy]`

The following parameters are unique to posting a message:

 * `message[recipient_id]` (required)
 The user ID of the recipient.

 * `message[parent_id]` (optional)
 If a reply, the ID of the message it is in reply to.


### Blocking ###
Some users may be blocked from messaging or following others.

If you GET the details of an individual user, there is a `messaging_enabled` flag indicating whether that user can be messaged, and likewise for the `following_enabled` flag

Each message in the inbox contains a `user[messaging_enabled]` flag showing if that message can be replied to.