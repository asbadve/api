# How to authenticate requests made to the audioboo.fm api

# API Authentication #

To make API calls that are marked as authenticated you will need to ensure your application has been authorized by a user. Authenticated calls will typically access or publish data that is restricted to that particular user.

## OAuth Scheme ##
The API supports the OAuth standard to make authenticated calls on behalf of a user. To find out more about the OAuth specification and to find a library that implements it in your language, see http://oauth.net/.

You should use OAuth 1.0A to make your requests.  You might like to examine our [example Ruby code](https://github.com/Audioboo/audioboo-ruby-oauth) to see how things are supposed to work.


## Consumer Keys ##
To make authenticated requests you'll need to get hold of a consumer-token key and secret. These are long seemingly random strings that ensure we can identify your application when it makes calls.

To register for key and token, head over to https://audioboo.fm/account/services and click "Request new API Key". This will ask for some information regarding the application you're writing and, once submitted, should provide you with the token key and secret.

## OAuth Request URLs ##
When configuring your OAuth library, you will require URLs to access the OAuth calls. As we use standard paths, most libraries should just request the site's base address, which is `http://api.audioboo.fm/`


For completeness, the three specific OAuth URLs are;

* Request Token URL: `http://api.audioboo.fm/oauth/request_token`

* Authorization URL: `http://api.audioboo.fm/oauth/authorize`

* Access Token URL: `http://api.audioboo.fm/oauth/access_token`

## Signing multipart uploads ##
Multipart requests should be signed according to the [OAuth Request Body Hash extension](http://oauth.googlecode.com/svn/spec/ext/body_hash/1.0/oauth-bodyhash.html).


## Private Authentication Scheme ##
We initially implemented the private scheme for the original iPhone application and it allows authenticated API calls to be made without being linked to a particular user. When posting a boo in this state it will appear as an anonymous boo on the site (i.e. from "The BooBot"). We record the source of clips and when linked in the future all past anonymous boos will be transferred to the User.

OAuth has no mechanism to allow authenticated but anonymous calls to be made, so any boo posted will immediately belong to a user.

If you're interested in using the private authentication scheme to mirror the behaviour of the iPhone application, contact info@audioboo.fm.
