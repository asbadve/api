## Audio Clips (Boos)##

### All audio clips ###

These return [paginated](https://github.com/audioboo/api/blob/master/sections/pagination.md) responses.

 * GET /audio_clips
  returns all boos in chronological order (most recent first)
 * GET /audio_clips?find`[`query`]`=*query*
  searches for boos matching the *query* search term.
  returns all boos in chronological order (most recent first)
 * GET /audio_clips/featured
  returns the editorially "featured" boos as appear on the web-site
 * GET /audio_clips/popular
  returns the most popular audio clips ordered by recent listens

### Tagged audio clips ###
This call will return a [paginated] response.

 * GET /tag/*tag*/audio_clips
  returns all the audio clips tagged with the specified tag.
  
###User's audio clips###
These calls will return [paginated] responses.

 * GET /users/*user_id*/audio_clips
  returns the audio clips uploaded by the user specified by *user_id*.

 * GET /audio_clips?username=*username*
  returns the audio clips uploaded by *username*.  If known, using the user's id is preferred, since it's guaranteed to never change.

 * GET /account/audio_clips 
  returns the audio_clips uploaded by the user linked to the OAuth access token used.

### User's followed clips ###
These calls will return [paginated] responses.

 * GET /users/*user_id*/audio_clips/followed
  returns the audio clips uploaded by users followed by the user specified by *user_id*.

 * GET /account/audio_clips/followed
  returns the audio clips uploaded by users followed by the user linked to the OAuth access token used.

### Clips by location ###

#### Filtering for clips with location ####
There is a feed of boos restricted only to those with a public location, which may be useful for generating maps of boos, etc.
This can be accessed using a call to the URL:

 * GET /audio_clips/located

#### Search by distance from point ####
If you want to get a list of boos increasing near a specific long/lat point you can call this:

 * GET /audio_clips/located`?`find`[`latitude`]`=*latitude*`&`find`[`longitude`]`=*longitude*

The results will be ordered by a function of recentness and closeness to the given point.

#### Search for boos "nearby" ####
You can search for clips nearby another clip:

 * GET /audio_clips/*clip_id*/nearby

Which will return clips in the same order as clips returned from a long/lat point. For this and the clips from point call you'll also get a "bearing" and "distance" tag in the returned XML for each result which will tell you the bearing and distance of each result from the query location, using the haversine approximation. Don't know if that is useful, but it's there!

#### Clips within a bounding box ####
You can request all the clips that fall within an arbitrary bounding box.

 * GET /audio_clips/located`?`BBOX=*west*,*south*,*east*,*north*

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

 * GET /audio_clips/*audio_clip_id*
  returns the details of the audio clip specified by *audio_clip_id*.

 * GET /audio_clips/*audio_clip_id*.mp3
  this will respond with a browser re-direct to the mp3 audio data for the audio clip specified by *audio_clip_id*

### Posting audio clips ###

POST /account/audio_clips

this will post an audio clip into the recent clips of the user linked to the OAuth access token used.

To post to a channel, you can use 

POST /channels/*channel_id*/audio_clips

which will post an audio clip to the specified channel.

The same parameters are used for either endpoint: 


 * `audio_clip[uploaded_data]` (required)
  The uploaded audio data as a multipart file, see [Audio Formats](https://github.com/audioboo/api/blob/master/sections/reference_index.md#audio-formats) and [File Uploads](https://github.com/audioboo/api/blob/master/sections/reference_index.md#file-uploads).

 * `audio_clip[uuid]` (recommended)
  A [universally unique identifier](http://en.wikipedia.org/wiki/Universally_unique_identifier), to aid the server in duplicate-detection.  The uuid must not contain spaces or a newline characters.

 * `audio_clip[uploaded_image]`
  The uploaded image data as a multipart file, see see [Image Formats](https://github.com/audioboo/api/blob/master/sections/reference_index.md#image-formats) and [File Uploads](https://github.com/audioboo/api/blob/master/sections/reference_index.md#file-uploads).

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

### Updating audio clips ###

You can update audio clips by sending a PUT request to the boo's location : 

PUT /audio_clips/*audio_clip_id*

It accepts the same parameters as those shown in the creation method.

### Deleting audio clips ###

You can mark audio clips for deletion by sending a DELETE request to the boo's location :

DELETE /audio_clips/*audio_clip_id*
