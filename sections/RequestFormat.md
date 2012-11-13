# How API Requests / Responses should be formatted

# API Call Format #

## Request URLs ##
Being a REST-style API, all calls are made to paths based on the resource you're accessing. For more specifics on individual resources, see the [ReferenceIndex API Reference].

For example, if you're trying to access a list of clips a user is following, you'll make HTTP `GET` request to:

{{{
http://api.audioboo.fm/users/12/audio_clips/followed.json
}}}

where 12 is the id of the user you're interested in and you want data returned in the JSON encoding. See [RequestFormat#Response_Encoding Response Encoding] below to find out what encodings we can use in responses.

If you were trying to upload a clip to the linked user, you'd make a HTTP `POST` to:
{{{
http://api.audioboo.fm/account/audio_clips
}}}

## Standard Parameters ##
To enable us to track what version of the API specification you have used to write your application, you should always include a `version` parameter along with the parameters of the API you are calling.

The current value of `version` is 200. If your app uses a version number that is no longer supported by the server, the server will respond with an appropriate error.

## Request Parameter Encoding ##
Parameters required by the API call can be submitted in one of a few ways:

 * [http://en.wikipedia.org/wiki/Query_string Query String Parameters]
 * Parameter data in HTML request body ([http://www.w3.org/TR/html401/interact/forms.html#h-17.13.4.1 W3C Spec]):
  * URL-encoded field data (application/x-www-form-urlencoded)
  * multipart/form-data (multipart/form-data)

 _NOTE:_ multipart/form-data _must_ be used when posting large fields, such as an uploaded audio-file.

## Response Encoding ##
We have internally simplified returned data into series of hashes, arrays and basic data types that can be easily represented in a variety of encoding formats. As mentioned above, you can request a particular format by changing the extension of the page you request. 

So for a JSON response, you'd call:
{{{
http://api.audioboo.fm/users/12/audio_clips/followed.json
}}}

yet, for a YAML response, you'd go for:
{{{
http://api.audioboo.fm/users/12/audio_clips/followed.yaml
}}}


The formats we currently support are;
 * [http://en.wikipedia.org/wiki/XML xml]
 * [http://en.wikipedia.org/wiki/YAML yaml]
 * [http://en.wikipedia.org/wiki/JSON json]
 * [http://en.wikipedia.org/wiki/JSON#JSONP jsonp]

 _NOTE:_ If you use JSON-P, you also need to supply a `callback` parameter which is used as the wrapper function when the data is returned.

## Response Envelope ##
When data is returned in the format you have requested, the root object is always a hash that acts as a response envelope allowing out-of-band data to be passed back to the application. As it currently stands, the server only returns an api-version key and the servers integer timestamp.

Any response data relating to the request made will _always_ be returned in the `body` element of this hash.

## Error Responses ##
TODO: Errors during processing

## Scheduled Downtime ##

TODO: Explain what the feeds will do when we bring the servers down. Example page?