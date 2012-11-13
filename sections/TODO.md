# Things in the pipeline...

# API Public Whiteboard / TODO List #

The official list is on the whiteboard on my right, but I'll try and keep this up-to-date so you know what to expect. If you comment on this page I'll hopefully get notified and add suitable suggestions...

## Crucial stuff ##

*_Documentation_* 

  Yes, yes I know, the reference in particular needs a whole load more documentation to be useful. Hopefully there is enough to get by for the time being, and you can always [Support email] me.

*Example Code / expected output*

  Contributions welcomed...

*Comments*

  Glaring omission from the current API, shouldn't take too long to get it sorted... Listing,   reading, writing and deleting comments. Standard stuff.

*Ratings*

  There isn't any public readout for the rating and it doesn't really affect anything, so this will probably hit the back-burner for the time being, but we'll add some mechanism to register a user's interest or dis-interest in boos ... at some point ... 

*Reporting*

  You can report offensive boos through the web-site, and I'll add a parallel call to the API.

*Chunked / Partial uploader*

  At the moment you need to upload an audio-clip, images and meta-data in a single call that is asking for failure, especially over 3G. I'm going to break these out (optionally) into a separate series of calls, so you can trickle data upto the server using the HTTP Range: header, and as soon as the data is uploaded, reference the files in the post-boo call.

*Remove old OAuth authentication path*

  Bit of a techy one, but the adoption of the OAuth Rev1.0a seems vague across sites so I kept the old authorization path in (passing the callback URL to the authorization call rather than the request token call, and adding in the PIN verifier). The new standard does seem adopted, so I'm going to drop the old path.

*Clean up validation responses*

  If you submit data, specifically to the audio clip posting then you might get error responses that reference fields internal to the database that might not exactly align with what you'd expect. I'll try and sort this out and document what validation errors look like in a more concrete way.

*Glaring error with 404 errors*

  If you call a non-existent path and, rightfully, append the .xml format specifier, then you'll get a confusing "Unsupported API format" error rather than a 404 error. You can confirm this by adding the ?fmt=xml to your call to see what the _actual_ error should be.

*Tag browsing*

  At the moment you can only see audio-clips for a tag. I'll add browsing for popular and related tags at some point.

## Fun suff ##
*XMPP Notifications*

  I'm overhauling how third-party notifications work in the front-end site, and as a part of this I'd like to add in XMPP PubSub style notifications of internal audio-boo events (such as boo published, etc). Anything to stop people polling!!

*HTTP Pings*

  Similar in vein to XMPP Notifications, I'd really like to disuade people from polling our (mostly) static feeds, so I'm going to add a HTTP ping for changes to various lists. This will start out simple, but hopefully develop so you can "subscribe" URLs to be pinged when specific data-sets change... Ideas welcomed...