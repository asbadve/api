# Audioboo Categories

Boos and channels are categorized into different areas.  You can obtain lists of them via the Categories API.

Get Categories
----
`GET /categories` Returns a list of categories used on Audioboo
Certain categories are only available for boos or for channels, by default this method only returns channel categories. You should filter the result set to only include the type you are interested in by using one of :
`GET /categories/channels`
`GET /categories/boos`
`GET /categories/all`

It is likely that in the future, the default filter on `GET /categories` will change to return all categories rather than just channel-categories.
