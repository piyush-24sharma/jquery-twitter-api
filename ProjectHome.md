jQuery Twitter API aims to give Web developers the ability to request Twitter public informations from a simple JavaScript function call. See Twitter API for more information http://apiwiki.twitter.com/.

_NB : informations requiring authentication are not accessible to JavaScript inside classical Web pages because of the [same origin policy restriction](https://developer.mozilla.org/en/Same_origin_policy_for_JavaScript)_


Methods can be of two forms depending on the type of requests :

  * $.twitter._optional-subapi.method_(success, _additionalParametersObject_);

  * $.twitter._optional-subapi.method_(_specificParameter_, success, _additionalParametersObject_);


The parameters are :
  1. _specificParameter_ : a string representing the query, example : "web", "sroucheray"... Some methods do not require this parameter some do.
  1. _success_ : A function to be called if the request succeeds. It must be of the form _function success(jsonData, textStatus)_
  1. _additionalParametersObject_ : An object containing additional parameters to handle the request. Almost all [jQuery Ajax options](http://docs.jquery.com/Ajax/jQuery.ajax#options) can be set in this object (exception are "data", "dataType", "jsonp", "success", "type" and "url")

# Usage example #
```
//Test Twitter : should return OK 
$.twitter.test(printSuccess);

//Search methods
$.twitter.search("test",printSuccess);
$.twitter.search.user("sroucheray",printSuccess);
$.twitter.search.repliesTo("sroucheray",printSuccess);
$.twitter.search.mentioned("sroucheray",printSuccess);
$.twitter.search.hashtag("35days",printSuccess);

//Trends methods
$.twitter.trends.current(printSuccess);
$.twitter.trends.daily(printSuccess);
$.twitter.trends.weekly(printSuccess);

//Public methods
$.twitter.statuses.publicTimeline(printSuccess);
$.twitter.statuses.show("123", printSuccess);
$.twitter.statuses.friends("42421507", printSuccess);

//Social Graph methods 
$.twitter.friends.ids("123", printSuccess);
$.twitter.followers.ids("123", printSuccess);

//Twitter API limitation check
$.twitter.account.rateLimitStatus(printSuccess);

function printSuccess(data, textStatus){
//Handle data as a JSON object
}
```

# JSONP and jQuery #
To work, the jQuery Twitter API need to use [JSONP](http://en.wikipedia.org/wiki/JSON#JSONP) callback.
By default, jQuery badly handle error when using AJAX request with JSONP callback. Including, the [JSONP for jQuery](http://code.google.com/p/jquery-jsonp/) extension before calling any jQuery Twitter API method will better handle error fallback without changing the API behavior. (Not including it will let the API works with the standards jQuery AJAX request).