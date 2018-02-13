# soal jan 2018 study notes for fetch and polyfill
#### compiled on feb 12 2018 

=========================
### fetch vs xmlhttprequest
=========================

#### client side http data requests




/*

 * Client-side HTTP requests three ways, using ES6 syntax.

 * 1. jQuery.ajax()

 * 2. Superagent

 * 3. Fetch API

 * 4. Bonus helper

 */ 



// 1. jQuery.ajax()

// http://api.jquery.com/jquery.ajax/

import jquery from 'jquery';



jquery.ajax({

  method: "GET",

  url: 'https://jsonplaceholder.typicode.com/users',

  headers: {

    'custom-head': 'custom ',

  },

  })

  .done((result) => {

    console.log(result);

  })

  .fail((jqXHR, textStatus, error) => {

    console.log(textStatus);

  });





// 2. Superagent

// https://github.com/visionmedia/superagent

import request from 'superagent';



request

  .get('https://jsonplaceholder.typicode.com/users')

  .set('custom-header', 'custom header value')

  .end((error, response) => {

    if (error) {

      console.log(error);

    } else {

      console.log(response.body);

    }

  });



// 3. Fetch API

// 'isomorphic-fetch' is optional. It will include a [Fetch API polyfill](https://github.com/github/fetch) 

// [if needed](http://caniuse.com/#feat=fetch) (e.g for IE).

import fetch from 'isomorphic-fetch'; 



  fetch('https://messaging.settled.co.uk/debug')

  .then(response => {

    // This response from a server could contain a HTTP error code but it will 

    // still end up here. To throw this as an error see checkFetchStatus() below

    // and uncomment the following:

    // checkFetchStatus(response)

    console.log(response);

  })

  .catch(error => {

    // Network or timeout error.

    console.log(error);

  });





// 4. Bonus: Fetch API respnse status check helper



/**

 * Check the status of a returned Fetch API call and throw an error if the 

 * server returns an error code.

 * See https://www.tjvantoll.com/2015/09/13/fetch-and-errors/

 */

function checkFetchStatus(response) {

  if (response.status >= 200 && response.status < 300) {

    return response;

  } else {

    const error = new Error(response.statusText);

    error.response = response;

    throw error;

  }

=== Source: https://gist.github.com/hedleysmith/15fa60fda5ef4369636a4b23e018dc8f ===


Source 2
========

fetch
- missing a builtin method to consume documents
- no way to set a timeout yet
- can't override the content-type header of the response
XHR
- there's no way to not send cookies
- can't return FormData instances
- doesn't have an equivalent to fetch's no-cors mode

=== Source: https://stackoverflow.com/questions/35549547/what-is-the-difference-between-the-fetch-api-and-xmlhttprequest?noredirect=1&lq=1 ===

Additional: 

Mozilla Docs on Fetch: https://hacks.mozilla.org/2015/03/this-api-is-so-fetching/

Pros and Cons of fetch vs xmlhttprequest: (from 2015) https://jakearchibald.com/2015/thats-so-fetch/

fetch support 2018: https://caniuse.com/#search=fetch

fetch github: https://github.com/github/fetch


 
============
||Polyfill||
============
Polyfill: What is a Polyfill?
A polyfill, or polyfiller, is a piece of code (or plugin) that provides the technology that you, the developer, expect the browser to provide natively. Flattening the API landscape if you will.
=== Source: https://remysharp.com/2010/10/08/what-is-a-polyfill === 

Transpiling vs polyfilling: https://hackernoon.com/polyfills-everything-you-ever-wanted-to-know-or-maybe-a-bit-less-7c8de164e423







