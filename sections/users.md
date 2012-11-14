## Users ##

### Lists of Users ###

 * GET /users
  this call requires exactly one of two parameters to find a specific user. The behavior if both parameters are supplied is undefined.

    `find[username]=*username*`

    will return _at most_ one user who has the specified user exactly. This is the recommended way to find an id for a named user.

   `find[query]=*query*`

   will perform a more flexible search for the query against the users on the system. It can return multiple users that match the query and you can use the `*` as a wildcard


### User details ###

 * GET /users/*user_id*
  This will return the details for the user specified by the *user_id* parameter.

 * GET /account
  This will return the details of the user linked to the OAuth access token.