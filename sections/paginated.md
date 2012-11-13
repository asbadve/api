# API Pagination

When fetching lists of entities from the api, the response is broken up into pages.  You can control the pagination with the following parameters : 

  *  `page[number]` - the page of results you'd like to return, starting at 1.
  *  `page[items]` - the number of results you'd like on each page.  This value is capped at 150.
  *  `max_time` - an optional unix timestamp of the most recent time you'd like pagination to start from.  This is used to stabilize pagination - if you're paging through sequential pages, you can record a start time and send that with each request, to ensure that boos created since you started paging don't shuffle your results around.  (Even so, this isn't a guarantee, and you should check for duplicate entity ids when fetching multiple pages).