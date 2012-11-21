## Playlists ##

### Lists of Users Playlists ###

 * GET /users/*user_id*/playlists

This call will return a list of users playlists.
  

### Playlist details ###

 * GET /playlists/*playlist_id*

This call will return a paginated detail view of the playlist and it's audio clip members.


### Create playlist (Authenticated) ###

 * POST /playlists
  
This call will create a playlist for the current authenticated user.

  Parameters accepted:

  * `playlist[title]` (required) Name of playlist
  * `playlist[image_data]` (optional) The uploaded image data as a multipart file, see see [Image Formats](https://github.com/audioboo/api/blob/master/sections/reference_index.md#image-formats) and [File Uploads](https://github.com/audioboo/api/blob/master/sections/reference_index.md#file-uploads).


### Update playlist (Authenticated) ###

 * PUT /playlists/*playlist_id*
  
This call will update a playlist details.

  Parameters accepted:

  * `playlist[title]` (required) Name of playlist
  * `playlist[image_data]` (optional) The uploaded image data as a multipart file, see see [Image Formats](https://github.com/audioboo/api/blob/master/sections/reference_index.md#image-formats) and [File Uploads](https://github.com/audioboo/api/blob/master/sections/reference_index.md#file-uploads).


### Deleting a playlist (Authenticated) ###

 * DELETE /playlists/*playlist_id*
  
This call will delete a playlist.


### Adding boos/clips to playlist (Authenticated) ###

 * POST /playlists/*playlist_id*/playlist_memberships
  
This call will add an audioclip to a playlist.

  Parameters accepted:

  * `playlist_memberships[audio_clip_id]` (required) 


### Removing boo/clip from playlist (Authenticated) ###

 * DELETE /playlists/*playlist_id*/memberships/*membership_id*
  
This call will remove an audioclip from a playlist.


### Updating the position of audioclip within the playlist (Authenticated) ###

 * POST /playlists/*playlist_id*/playlist_memberships/*membership_id*
  
This call will update the audioclip position within the playlist.

  Parameters accepted:

  * `playlist_memberships[position]` (required) 

