# MUST DO:
  - https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching
  - https://www.w3.org/2005/MWI/BPWG/techs/CachingWithETag.html
  - https://devcenter.heroku.com/articles/increasing-application-performance-with-http-cache-headers
  - https://classroom.udacity.com/courses/ud884/lessons/1464158641/concepts/14734291220923#
## project 5
  - https://en.wikipedia.org/wiki/Tim_Berners-Lee
  - https://www.w3.org/People/Berners-Lee/
  - https://www.ted.com/speakers/tim_berners_lee
  - https://en.wikipedia.org/wiki/Standard_Generalized_Markup_Language
  - https://en.wikipedia.org/wiki/HTML
  - https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol
  - http://www.restapitutorial.com/lessons/httpmethods.html
  - https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch
  - https://developers.google.com/web/updates/2015/03/introduction-to-fetch?hl=en
  - http://nc110.sourceforge.net/
  - https://en.wikipedia.org/wiki/Netcat
  - https://en.wikipedia.org/wiki/List_of_HTTP_header_fields
  - https://badssl.com/
  - https://developer.mozilla.org/en-US/docs/Web/Security/Mixed_content
  - https://developer.mozilla.org/en-US/docs/Web/Security/Mixed_content/How_to_fix_website_with_mixed_content
  - http://httparchive.org/trends.php?s=All&minlabel=Nov+15+2010&maxlabel=May+15+2016
  - http://dev.chromium.org/spdy/spdy-whitepaper
  - https://http2.github.io/http2-spec/compression.html
  - https://www.w3.org/Security/wiki/Same_Origin_Policy
  - https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS#Preflighted_requests
  - https://en.wikipedia.org/wiki/Cross-site_scripting
# The internet
  -
## The Web
  - is just a small part of the internet
  - is a platform for web developers to publish ideas to the world
  - it is clients (browsers) communicating with servers
  - its all about publishing and accessing documents/information
  - history:
    + tim berners lee created the web in order for researchers to easily transfer documents between each other
    + he created a subset of SGML and called it HTML
    + he created HTTP, which is designed to transfer HTML
  - architecture
    - HTTP > TCP > IP > ethernet
      + TCP: impacts how we format our requests for best performance
        - allows us to have multiple streams of data between connections
        - each stream is distinguished by PORT numbers
        - 3 way handshake to make a new connection on http
          1. i ask you: i want to talk
          2. you ask me: you heard i want to talk
          3. i tell you: yes, that is correct
          4. for https, and additional TLS handshake must be executed
      + IP: determines how we talk to other machines on the net
### Same Origin policy
  - Javascript is not allowed to access the origin of any other origin than its own
  - origin scheme: change any of the following and you are on a different origin
    1. data scheme: the protocol, e.g. http / https
    2. hostname: the domain, e.g. localhost, www.udacity.com
    3. port: e.g. :3000, :80
  - rules specific to Same Origin policy
    + same origin policy is enforced by the browser
    + this is so you cannot request data from other origins and make modifications on a users' behalf
    1. you cannot make fetch requests to other origins
      - 'Access-Control-Allow-Origin' must be enabled on the requested resource if you want to bypass this rule
      - you can also set the request's mode to 'no-cors' to bypass this rule
    2. you cannot inspect iframes/windows with javascript on different origins
    + exceptions to the above rules
      1. you can get scripts/images, etc from other origins
        - however, you cannot interactive with them the same way
          1. you cant inspect the pixel details of images via javascript
          2. you cant inspect the script content via javascript
### Cross Origin Resource Sharing (CORS)
  - is a set of HTTP headers to allow sharing resources across origins
    + the server specifies a set of origins that are allowed to access its resources
    + the request headers:
      1. GET /some/resource/blah
      2. HOST: api.someOtherOrigin.com
      3. Referer: your.site.com
    + the response headers:
      1. HTTP/1.1 OK
      2. DATE: December 12, 1985 00:22:54 GMT
      3. Access-Control-Allow-Origin: your.site.com
  + Preflight Requests:
    - uses the OPTIONS header to inform the server that the client only wants to request what http methods are allowed
    - you can view these in the network tab, any request which uses the OPTIONS header (check methods tab in network) is a preflight request
  - JSONP is one way to get around same origin policy
    1. you request a JSONP API and provide a callback function
    2. the API calls your callback function with the script contents as its only parameter
    2. since the callback function is from your origin, you can access the script contents, effectively bypassing same  origin policy
### Cross Site Request Forgery (CSRF)
  - CSRF is a token put on a form by the server, and is also stored server slide
    + if someone submits the form, it checks the CSRF token against the one it has stored and only executes the request if the tokens match
### Cross Site Scripting (XSS)
  - when javascript is executed in another site via some input field, and now has access to all of the sites data
  - you must validate all user input on the client, and more importantly, on the server
### performance
  - time to first byte: TTFB: the it takes to receive the first byte after making a request
  - head of line blocking: when subsequent requests need to wait on prior requests TTFB before being made
    + i.e.  request to / will eventually request css, images, etc., those css images are blocked until / is parsed
    + in HTTP/1.1, browsers open up to 6 paralel connectinos to handle this problem
### HTTP Requests and Responses:
#### Requests
  - request structure: only requires method and host header
    + method: GET, POST, etc, tells the server what the client wants to do
      - GET /path/to/document.jpg HTTP/1.1
      - method, document path, http version
    + Headers
      - Host: where the server is located
      - User Agent: type of client
      - Connection:
      - Accept: what type of document format the client accepts
      - If-None-Match: the version already available in client
  -
##### Request Methods
  + GET: retriev stuff
  + POST: create new stuff
    - the response should redirect to the newly created stuff
  + PUT: update existing stuff
  + DELETE: duh!
  + HEAD: get the headers of a file, without the actual file
    - useful for:
      + checking if there is enough space to store the response
      + if your cached version is still up to date
      + only useful for very large files, as you will incur two round trips
  + OPTIONS: get a list of methods that are accepted on the current URL
    - Post: you should respond to post requests with a redirect so that reloading the page doesnt cause an additional post
##### Request Headers
  - Connection: Keep Alive
    + informs the server to keep the connection open after it returns the response
    + this allows you to send multiple requests to the same server, without having to go through the TCP 3 way handshake each time
#### Responses
  - response structure: only requires http version line and content-length header
    + HTTP/1.1 200 OK
      - http version, status code, status text
    + Headers
      - Content-Length:
      - Server:
      - Etag:
      - Content-Type:
      - Date:
    + Binary data: the actual data
##### Response Headers
  - https://en.wikipedia.org/wiki/List_of_HTTP_header_fields
  - Content-Length
    + is a header that must be contained in every response and tells the browser the size of the body in the response. This way the browser knows how many bytes it can expect to receive after the header section and can show you a meaningful progress bar when downloading a file.
  - Content-Type
    + is also a non-optional header and tells you what type the document has. This way the browser knows which parsing engine to spin up. If it's an image/jpeg, show the image. It’s text/html? Let’s parse it and fire off the necessary, additional HTTP requests. And so on.
  - Last-Modified
    + is a header that contains the date when the document was last changed. It turned out that the Last-Modified date is not very reliable when trying to figure out if a document has been changed. Sometimes developers will uploaded all files to the server after fixing something, resetting the Last-Modified date on all files even though the contents only changed on a subset. To accommodate this, most servers also send out an ETag.
  - ETag
    + stands for entity tag, and is a unique identifier that changes solely depending on the content of the file. Most servers actually use a hash function like SHA256 to calculate the ETag.
      1. enables efficient resource update checks - no data is transferred if the resource has not changed

  - Cache-Control
    + is exactly what it sounds like. It allows the server to control how and for how long the client will cache the response it received. Cache-Control is a complex beast and has a lot of built-in features. 99% of the time, you only need the “cacheability“ and the “max-age”.

  - If-Modified-Since
    + permits the server to skip sending the actual content of the document if it hasn’t been changed since the date provided in that header. Is there something similar for ETags? Yes there is! The header is called If-None-Match and does exactly that. If the ETag for the document is still matching the ETag sent in the If-None-Match header, the server won’t send the actual document. Both If-None-Match and If-Modified-Since can be present in the same request, but the ETag takes precedence over the If-Modified-Since, as it is considered more accurate.
# REST: REpresentational State Transfer
## Basics
  - basic entitires are collections and entities inside those collections
    + GET <collection name>/<item name>
# http
  - is public, and anyone can eaves drop on your requests and responses
  - https://en.wikipedia.org/wiki/Firesheep
# https
  - is secured, no one can eaves drop on your requests or responses
    + it encrypts the requests and responses between server and client
    + authentication: this stops man in the middle attacks
  - man in the middle attacks
    + someone inserts their server in between you and the server you want
    + even though its https, there intercept, and relay to your requested server, and still hijack your requests and responses
  - HTTPS = http + TSL (formerlly ssl)
## TLS (formerlley ssl)
  + TLS: transport layer security, can be use with any protocol, e.g. FTP has FTPS
    - encrypts communcation via a certificate issued by a certificate authority
      + metadata about the server
      + an encrypted fingerprint to decode communication
      + certificates validates a server, and the owner of the server
  + see all certificates: chrome://settings/search#Certificates
  + Encryption
    - symetric encryption (i.e. public key encryption): you encrypt some data with a key, pass the data to someone else, who has a symetrical key for unlocking the data
      + http://hitachi-id.com/concepts/asymmetric_encryption.html
    - browser encryption:
      + encryption key: is public (i.e. the public key), so anyone can send an encrypted message
      + decryption key: is private (i.e. the private key), so only the client can decrypt the message
  + Hashing
    - the process of transforming data into a short representation of the original data
      + the smallest change in the original data will have enormous changes in the hash
        - if two documents yield the same hash, it is a super high probability they are the same document
    - hashing requirements:
      1. should be impossible to undo the hash transformation
      2. should be impossible to create two identical hashes from distinct documents
    - types of hashing:
      + the number says how big the hash is in bits
        - no matter how big the document is that you pass in, you will always get the # of bits indicated
      + SHA1:
      + SHA256:
      + SHA512:
### TLS handshake
  1. server sends client the certificate
    - public key
    - domain the certificate is for
    - signature by the certificate authority
  2. client confirms information
    - is domain correct?
    - is the authority signature valid?
      - all browsers have a collection of a certificate authorities including their public keys
  3. client generates a random key for symmetric encryption to be used from here forward
    - the browser encrypts the random key with the servers public key
    - symmetric is faster than assymetric encryption
    - only the server can decrypt the random key with the  private key and access the information
### TLS (ssl) errors
  - certificate authority signature is invalid
  - server is unable to communicate after switching to ssymetric encryption
  - certificate expires (they have expiration dates)
  - certificate is valid, but the server is invalid
### Certificates
  - An invalid certificate is where the URL for the certificate does not match the URL in the browser's address bar
  - an invalid signature, is when the decrypted hash does not match the one signed by the certifcate
  - Certificate Authorities: sign (validate) certificates
  - To speed up the encrypting and decrypting process, only the HASH is encrypted,
  - Self signed certificates:
    + these certificates refer to themselves as their own certificate authority
    + browsers will complain
### Mixed Content
 - when a TLS secure origin requests non secure content
 - you can get pass this by only consuming securing content
# HTTP2
  - head of line requests: when one request is blocking others from completing
    + a browser will open at most 6 simultaneous connections to a server
    + you will have to wait for a round trip (req + res) to complete before another request can happen
  - benefits
    + header compression
      - all streams share the browser compressor, so headers never have to be sent twice
    + multiplexing: combining multiple connections into a single connection via streams
      - streams are split up into frames
      - resolves head of line blocking
    + concatenating JS/CSS files is no longer necessary since head of line blocking is gone
      - its also worse to serve one big file, vs a lot of small files, for sites that use caching
        + you are forcing your users to download the concated files, instead of the single file that changed

# Proxy
  - these are servers that sit between you and some other server
  - useful for:
    1. adding additinoal compression
    2. downsampling images
    3. doing aggressive caching

# CACHING

  - **what is it**
    - temporarily storing content/responses from previous requests, core part of content delivery strategy implemented with http protocol
    - components throughout the delivery path can cache items to speed up subsequent requests, subject to caching policies declared for the content
  - **benefits**
    - decreased network costs: when content is cached closer to consumer, requests will not cause as much additional network activity beyond the cache
    - improved responsiveness: caching enables content to be retrieved faster
    - increased performance on the same hardware: for the server where the content originated, more performance can be squeezed by allowing aggressive caching.
    - availability of content during network interruptions: with certain caching policies, caching can be used to serve content to end users when it may be unavailable from origin servers
  - **terminology**
    - origin server: original location of content, responsible for serving all content that cannot be retrieved from a cache along the request route and for setting the caching policy for all content
    - cache hit ratio: a cache's affectiveness measured in terms of its cache hit ratio or hit rate
    + cached requests / total requests
    + a high cache hit ratio is usually the desired outcome
    - freshness: whether an item within a cache is still considered a candidate to serve to a client
    + content in a cache will only be used to respond if it is within the freshness time frame specified by the caching policy
    - stale content: items in cache expire according to the cache freshness settings in the cache policy. expired content is stale
    + origin servers must be re-contacted to retrieve the new content or at least verify that the cached content is still accurate
    - validation: Stale items in the cache can be validated in order to refresh their expiration time. Validation involves checking in with the origin server to see if the cached content still represents the most recent version of item.
    - Invalidation: removing content from the cache before its specified expiration date. This is necessary if the item has been changed on the origin server and having an outdated item in cache would cause significant issues for the client.
  - **types of caches**
    - application cache:
    - memory cache:
    - Intermediary caching proxies: Any server in between the client and your infrastructure can cache certain content as desired. These caches may be maintained by ISPs or other independent parties.
    - Reverse Cache: Your server infrastructure can implement its own cache for backend services. This way, content can be served from the point-of-contact instead of hitting backend servers on each request.
    - web/browser cache: Web browsers themselves maintain a small cache.
      + core design of the http protocol meant to minimize network traffic while improving the perceived responsiveness of the system as a whole
      + *how it works*
        1. caching the HTTP responses for requests according to specified rules
        2. subsequent requests for cached content are fullfilled from a cache closer tot he user instead of sending the requests all the way back tot he web server
  - **what can be cached**:
    - cache friendly items: anything that is static/near-static
      + images, especially static images like icons, logos, etc
      + stylesheets
      + javascript files
      + downloadable content
      + media files
    - cache unfriendly items: anything that is dynamic, or is changed frequently, must be cached with care
      + html pages
      + rotating images, e.g. user profile pics
      + content requested within authentication cookies
    - cache hatred items: things you should never cache
      + assets related to sensitive data ( e.g. banking )
      + user specific content and frequently changed
  - **cache headers**
    - caching policy: determined by content owner and specified via specific http headers
      + caching entity decides how much to cache, but never more than specified by caching policy
    - Http headers related to caching
      + Expires: sets a time in the future when the content will expire. replaced by Cache-Control: max-age, but this should still be used as fallback for old browsers.
        1. Any requests for the same content will have to go back to the origin server.
      + Cache-Control: replacement for the Expires header but is best to use both
        - enumerated values:
          + **for all cache types**
            1. no-cache: This instruction specifies that any cached content must be re-validated on each request before being served to a client. This, in effect, marks the content as stale immediately, but allows it to use revalidation techniques to avoid re-downloading the entire item again.
            2. no-store: This instruction indicates that the content cannot be cached in any way. This is appropriate to set if the response represents sensitive data.
            3. public: This marks the content as public, which means that it can be cached by the browser and any intermediate caches. For requests that utilized HTTP authentication, responses are marked private by default. This header overrides that setting.
            4. private: This marks the content as private. Private content may be stored by the user's browser, but must not be cached by any intermediate parties. This is often used for user-specific data.
            5. max-age: This setting configures the maximum age that the content may be cached before it must revalidate or re-download the content from the origin server. In essence, this replaces the Expires header for modern browsing and is the basis for determining a piece of content's freshness. This option takes its value in seconds with a maximum valid freshness time of one year (31536000 seconds).
            6. must-revalidate: This indicates that the freshness information indicated by max-age, s-maxage or the Expires header must be obeyed strictly. Stale content cannot be served under any circumstance. This prevents cached content from being used in case of network interruptions and similar scenarios.
            7. no-transform: This option tells caches that they are not allowed to modify the received content for performance reasons under any circumstances. This means, for instance, that the cache is not able to send compressed versions of content it did not receive from the origin server compressed and is not allowed.
          + **only for intermediary caches**
            1. s-maxage: This is very similar to the max-age setting, in that it indicates the amount of time that the content can be cached. The difference is that this option is applied only to intermediary caches. Combining this with the above allows for more flexible policy construction.
            2. proxy-revalidate: This operates the same as the above setting, but only applies to intermediary proxies. In this case, the user's browser can potentially be used to serve stale content in the event of a network interruption, but intermediate caches cannot be used for this purpose.
          + **gotchas**
            1. *no-cache* and *no-store* should not be used together
              - if they are, *no-store* wins
            2. For responses to unauthenticated requests, *public* is implied
            3. For responses to authenticated requests, *private* is implied
      + Etag: used with cache validation. The origin will either tell the cache that the content is the same, or send the updated content (with the new Etag).
        1. The origin can provide a unique Etag for an item when it initially serves the content.
        2. When a cache needs to validate the content it has on-hand upon expiration, it can send back the Etag it has for the content.
      + Last-Modified: This header specifies the last time that the item was modified.
        1. This may be used as part of the validation strategy to ensure fresh content.
      + Content-Length: Certain software will refuse to cache content if it does not know in advanced the size of the content it will need to reserve space for.
      + Vary: A cache typically uses the requested host and the path to the resource as the key with which to store the cache item. this provides you with the ability to store different versions of the same content at the expense of diluting the entries in the cache.
        1. used to tell caches to pay attention to an additional header when deciding whether a request is for the same item.
        2. This is most commonly used to tell caches to key by the Accept-Encoding header as well, so that the cache will know to differentiate between compressed and uncompressed content.
      + Accept-Encoding: This is needed to correctly serve items to browsers that cannot handle compressed content and is necessary in order to provide basic usability.
      + User-Agent:
  - caching policies:
    - purpose:
      1. aim to balance between implementing long-term caching and responding to the demands of a changing site.
      2. keep the cache hit-ration as high as possible while never serving stale content to users
    - issues:
      1. dynamically generated user content, sensitive data, should not be cached
    - questions:
      1. how should data that is not yet passed its expiration date, but has become stale due to new content availibity, be handled?
    - recommendations:
      + split your content into 3 buckets: The goal is to move content into the first categories when possible while maintaining an acceptable level of accuracy.
        1. Aggressively cached items
        2. Cached items with a short freshness time and the ability to re-validate
        3. Items that should not be cached at all
      + general recs
        1. Establish specific directories for images, css, and shared content: Placing content into dedicated directories will allow you to easily refer to them from any page on your site.
        2. Use the same URL to refer to the same items: Since caches key off of both the host and the path to the content requested, ensure that you refer to your content in the same way on all of your pages.
        3. Use CSS image sprites where possible: CSS image sprites for items like icons and navigation decrease the number of round trips needed to render your site and allow your site to cache that single sprite for a long time.
        4. Host scripts and external resources locally where possible: If you utilize javascript scripts and other external resources, consider hosting those resources on your own servers if the correct headers are not being provided upstream. Note that you will have to be aware of any updates made to the resource upstream so that you can update your local copy.
        5. Fingerprint cache items: For static content like CSS and Javascript files, it may be appropriate to fingerprint each item. This means adding a unique identifier to the filename (often a hash of the file) so that if the resource is modified, the new resource name can be requested, causing the requests to correctly bypass the cache. There are a variety of tools that can assist in creating fingerprints and modifying the references to them within HTML documents.
        6. Always provide validators: Validators allow stale content to be refreshed without having to download the entire resource again. Setting the Etag and the Last-Modified headers allow caches to validate their content and re-serve it if it has not been modified at the origin, further reducing load.
      + item type recs
        1. Allow all caches to store generic assets:
        2. Allow browsers to cache user-specific assets: For per-user content, it is often acceptable and useful to allow caching within the user's browser. While this content would not be appropriate to cache on any intermediary caching proxies, caching in the browser will allow for instant retrieval for users during subsequent visits.
        3. Make exceptions for essential time-sensitive content: If you have content that is time-sensitive, make an exception to the above rules so that the out-dated content is not served in critical situations. For instance, if your site has a shopping cart, it should reflect the items in the cart immediately. Depending on the nature of the content, the no-cache or no-store options can be set in the Cache-Control header to achieve this.
        4. Set long freshness times for supporting content: generally appropriate for items like images and CSS that are pulled in to render the HTML page requested by the user. Setting extended freshness times, combined with fingerprinting, allows caches to store these resources for long periods of time.
        5. Set short freshness times for parent content: In order to make the above scheme work, the containing item must have relatively short freshness times or may not be cached at all. This is typically the HTML page that calls in the other assisting content. The HTML itself will be downloaded frequently, allowing it to respond to changes rapidly. The supporting content can then be cached aggressively.

## CDN
  - content delivery network: system of distributed servers that deliver assets to a user based on geographic locations of the user, the origin of the assets, and a content delivery server
    + the closer the CDN server to the user geographically, the faster the content will be dleivered to the user.
    s