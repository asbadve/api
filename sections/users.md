## Users ##

### Lists of Users ###

 * `GET /users`
  this call requires exactly one of two parameters to find a specific user. The behavior if both parameters are supplied is undefined.

    `find[username]=*username*`

    will return _at most_ one user who has the specified user exactly. This is the recommended way to find an id for a named user.

   `find[query]=*query*`

   will perform a more flexible search for the query against the users on the system. It can return multiple users that match the query and you can use the `*` as a wildcard


### User details ###

 * `GET /users/*user_id*`
  This will return the details for the user specified by the *user_id* parameter.

 * `GET /account`
  This will return the details of the user linked to the OAuth access token.

```json
{
    "body": {
        "user": {
            "counts": {
                "audio_clips": 98, 
                "favorites": 114, 
                "followers": 53, 
                "followings": 67
            }, 
            "username": "jdelStrother",
            "full_name": "Jonathan del Strother", 
            "id": 5, 
            "limits": {
                "duration": 300, 
                "parallel": true, 
                "trickle": true
            },  
            "following_enabled": true,
            "messaging_enabled": true,
            "profile_description": "Audioboo dev, general code monkey.", 
            "profile_location": "London", 
            "urls": {
                "profile": "http://audioboo.fm/jdelStrother", 
                "website": "http://audioboo.fm"
            }, 
        }
    }, 
```    

### Updating your profile

  `PUT /account` accepts the following parameters:
  
  * `user[profile_name]` - the user's full name, for display purposes
  * `user[profile_location]` - geographic location
  * `user[profile_description]` - profile description, limited to 255 characters
  * `user[profile_website_url]` - the user's website address
  * `user[profile_picture_data]` - a profile image, as a [multipart file](https://github.com/audioboo/api/blob/master/sections/reference_index.md#file-uploads)
  
