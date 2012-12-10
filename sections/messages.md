## Messaging ##

All of these calls require an [authenticated user](https://github.com/audioboo/api/blob/master/sections/authentication.md).

### Inbox ###

The messages in the user's inbox. [Paginated](https://github.com/audioboo/api/blob/master/sections/pagination.md) and in chronological order (most recent first)
 * GET /account/inbox

### Message details ###

 * GET /account/messages/*message_id*
 returns the details of the message specified by *message_id*.

### Post message ###
This will send a message to another user (from the authenticated user).

 * POST /account/outbox

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

### Delete a message ###

 * DELETE /account/messages/*message_id*

This will delete the message specified by *message_id*.
