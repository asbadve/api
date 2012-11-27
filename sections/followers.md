## Listing followers / following users ##
Just to clarify:

Followers = users who have chosen to follow a user

Followings = users who a specific user is following

 * `GET /users/*user_id*/followings`
 * `GET /account/followings`

 * `GET /users/*user_id*/followers`
 * `GET /account/followers`

You can specify a `find[user_id]` parameter to limit the results to a particular set of users. To, for example, find out if stephen fry is following you, you'd call:

`GET /account/followers?find[user_id]=11`

You can supply multiple, comma-separated id's to restrict to a series of users, to find if any of the Audioboo team are following you, try:

`GET /account/followers?find[user_id]=12,17,5,30,16`

### Creating and Deleting followings ###

 * `POST /account/followings`
 * `DELETE /account/followings`

  Both of these calls require a single parameter `following_user_id` which is the id of the user to follow or un-follow.
