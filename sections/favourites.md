## Favourites ##

### User Favourites ###

 * GET /users/*user_id*/audio_clips/favourites
 * GET /account/audio_clips/favourites (Authenticated)
 * GET /account/favourites (Authenticated)

These will return a paginated response of the users favourite audio clips


### Get users who favourited an audio clip ###

 * GET /audio_clips/*audio_clip_id*/favourites

This will return a paginated response with the users who favourited an audio clip


### Favourite an audio clip ###

 * POST /audio_clips/*audio_clip_id*/favourites (Authenticated)

This will favourite an audioclip for the authenticated user, returns a 201 response


### Un-favourite an audio clip ###

 * DELETE /audio_clips/*audio_clip_id*/favourites (Authenticated)

This will un-favourite an audioclip for the authenticated user, returns a 200 response
