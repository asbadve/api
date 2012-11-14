# How API Requests / Responses should be formatted

# API Call Format #

## Request URLs ##
Being a REST-style API, all calls are made to paths based on the resource you're accessing. For more specifics on individual resources, see the [API Reference](https://github.com/audioboo/api/blob/master/sections/reference_index.md).

For example, if you're trying to access a list of clips a user is following, you'll make HTTP `GET` request to:

`http://api.audioboo.fm/users/12/audio_clips/followed`

where 12 is the id of the user you're interested in.  See [Response Encoding](https://github.com/audioboo/api/blob/master/sections/request_formats.md#Response_Encoding) below to find out what encodings we can use in responses.

If you were trying to upload a clip to the linked user, you'd make a HTTP `POST` to:
`http://api.audioboo.fm/account/audio_clips`

## Standard Parameters ##
To enable us to track what version of the API specification you have used to write your application, you should always include a `version` parameter along with the parameters of the API you are calling.

The current value of `version` is 200. If your app uses a version number that is no longer supported by the server, the server will respond with an appropriate error.

## Request Parameter Encoding ##
Parameters required by the API call can be submitted in one of a few ways:

  * [Query String Parameters](http://en.wikipedia.org/wiki/Query_string)
  * Parameter data in HTML request body ([W3C Spec](http://www.w3.org/TR/html401/interact/forms.html#h-17.13.4.1)):
  * URL-encoded field data (application/x-www-form-urlencoded)
  * multipart/form-data (multipart/form-data)

 _NOTE:_ multipart/form-data _must_ be used when posting large fields, such as an uploaded audio-file.

## Response Encoding ##
We have internally simplified returned data into series of hashes, arrays and basic data types that can be easily represented in a variety of encoding formats.  You can request a particular format using the HTTP Accept header, or by specifying the extension in the URI.  By default, json will be returned.

Thus, both the following commands are equivalent:
```
  curl http://api.audioboo.fm/audio_clips.xml
  curl -H"Accept: application/xml" http://api.audioboo.fm/audio_clips
```


We currently support  [json](http://en.wikipedia.org/wiki/JSON), [jsonp](http://en.wikipedia.org/wiki/JSON#JSONP),  [xml](http://en.wikipedia.org/wiki/XML), and [yaml](http://en.wikipedia.org/wiki/YAML).


_NOTE:_ If you use JSON-P, you also need to supply a `callback` parameter which is used as the wrapper function when the data is returned.

## Response Envelope ##
When data is returned in the format you have requested, the root object is always a hash that acts as a response envelope allowing out-of-band data to be passed back to the application. As it currently stands, the server only returns an api-version key and the servers integer timestamp.

Any response data relating to the request made will _always_ be returned in the `body` element of this hash.

## Response Status Codes ##
The response status code will follow [RFC2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).  All successful requests will return a 2xx HTTP status code, i.e. 200 for a normal request, 201 for a request in which an entity is created (such as an Audio Clip).

For failed requests, the server will typically return a suitable status value. If there is an internal server failure, for example, you will receive a 500 status code which should be presented to the user as a transient failure that should resolve itself at some point.

API failures caused by errors in the request will have two HTTP headers added to the server’s response,  `X-Audioboo-Error_code` and `X-Audioboo-Error_description`. The failure in this case is due to a failure between the client and the server, such as invalid signature or disabled service or source keys on the server.

A special case to this is the Audioboo error code 800, which indicates that the API version attached to the request sent is out of date and not supported by the server. In this case, it would be a wise idea to display the description sent by the server directly to the user as this will probably contain instructions on updating the client. No further attempts should be made to communicate with the server as they will result in the same response.