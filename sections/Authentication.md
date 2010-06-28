#summary How to authenticate requests made to the audioboo.fm api

= API Authentication =

To make API calls that are marked as authenticated you will need to ensure your application has been authorized by a user. Authenticated calls will typically access or publish data that is restricted to that particular user.

We currently support two schemes of authentication, OAuth and a private scheme. All of the API calls are accessible from either scheme, the only discernible difference is when posting a boo through the API.

== Private Authentication Scheme == 

We initially implemented the private scheme for the original iPhone application and it allows authenticated API calls to be made without being linked to a particular user. When posting a boo in this state it will appear as an anonymous boo on the site (i.e. from "The BooBot"). We record the source of clips and when linked in the future all past anonymous boos will be transferred to the User.

OAuth has no mechanism to allow authenticated but anonymous calls to be made, so any boo posted will immediately belong to a user.

If you're interested in using the private authentication scheme to mirror the behaviour of the iPhone application, contact support@audioboo.fm or thomas (at) bestbefore.tv.

== OAuth Scheme == 
The public API supports the OAuth standard to make authenticated calls on behalf of a user. To find out more about the OAuth specification and to find a library that implements it in your language, see [http://oauth.net/].

<font color=red>
*NOTE:* As it stands, the server will respond to both OAuth 1.0 Rev. A and OAuth1.0 requests (i.e. with and without the PIN based desktop workflow d the oauth_verifier response). I'm not entirely sure of the state of the transition to 1.0rev A - so staying backwards compatible for the time being.
</font>

== Consumer Keys == 
For either scheme, you'll need to get hold of a consumer-token key and secret. These are long seemingly random strings that ensure we can identify your application when it makes calls.

To register for key and token, head over to [http://audioboo.fm/account/services] and click "Request new API Key". This will ask for some information regarding the application you're writing and, once submitted, should provide you with the token key and secret.

== OAuth Request URLs == 
When configuring your OAuth library, you will require URLs to access the OAuth calls. As we use standard paths, most libraries should just request the site's base address, which is 
{{{
http://api.audioboo.fm/
}}}


For completeness, the three specific OAuth URLs are;

* Request Token URL:
{{{
http://api.audioboo.fm/oauth/request_token
}}}

* Authorization URL:
{{{
http://api.audioboo.fm/oauth/authorize
}}}

* Access Token URL:
{{{
http://api.audioboo.fm/oauth/access_token
}}}

== Signing multipart uploads ==
Multipart requests should be signed according to the [http://oauth.googlecode.com/svn/spec/ext/body_hash/1.0/oauth-bodyhash.html OAuth Request Body Hash extension].