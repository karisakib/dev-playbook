## API Design Rules

Rule: Forward slash separator (/) must be used to indicate a hierarchical relationship

```plain
http://api.canvas.restapi.org/shapes/polygons/quadrilaterals/squares
```

Rule: A trailing forward slash (/) should not be included in URIs

It may cause confusion and there is no semantic value to it. a REST API must generate and communicate clean URIs and should be intolerant of any client’s attempts to identify a resource imprecisely.

Rule: Hyphens (-) should be used to improve the readability of URIs. Anywhere you would use a space or hyphen in English, you should use a hyphen in a URI.

```plain
/my-first-blog-post
```

Rule: Underscores (\_) should not be used in URIs.

Depending on the application’s font, the underscore (\_) character can either get partially obscured or completely hidden by this underlining.

```plain
/my_first_blog_post
```

Rule: Use Lowercase Letters for readability.

```plain
/my-first-blog-post
```

Rule: File extensions should not be included in URIs to make paths cleaner.

```plain
/docs/financial-report-2025
```

Rule: Consistent subdomain names should be used for your APIs

```plain
api.example.com
```

Rule: Consistent subdomain names should be used for your client developers

This will help on-board new clients with documentation, forums, and self-service provisioning of secure API access keys.

```plain
dev.example.com
```

##### Rule: A singular noun should be used for document names

See this example: http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players/claudio

##### Rule: A plural noun should be used for collection names

Because collections contain more than one record or piece of data.

##### Rule: A plural noun should be used for store names

See this example: http://api.music.restapi.org/artists/mikemassedotcom/playlists

##### Rule: A verb or verb phrase should be used for controller names

See this example: /register

##### Rule: Variable path segments may be substituted with identity-based values.

The URI Template syntax allows designers to clearly name both the static and variable segments. Each substitution may use a numeric or alphanumeric identifier.
See this example: http://api.soccer.restapi.org/leagues/{leagueId}/teams/{teamId}/players/{playerId}

##### Rule: CRUD function names should not be used in URIs

##### Rule: The query component of a URI may be used to filter collections or stores

##### Rule: The query component of a URI should be used to paginate collection or store results

##### Rule: GET must be used to retrieve a representation of a resource

##### Rule: HEAD should be used to retrieve response headers.

HEAD returns the same response as GET, except that the API returns an empty body. Clients can use this method to check whether a resource exists or to read its metadata.

##### Rule: PUT must be used to both insert and update a stored resource

##### Rule: PUT must be used to update mutable resources

##### Rule: POST must be used to create a new resource in a collection

##### Rule: POST must be used to execute controllers

##### Rule: DELETE must be used to remove a resource from its parent

If an API wishes to provide a “soft” delete or some other state-changing interaction, it should employ a special controller resource and direct its clients to use POST instead of DELETE to interact.

##### Rule: 202 (“Accepted”) must be used to indicate successful start of an asynchronous action

A 202 response is typically used for actions that take a long while to process.
Controller resources may send 202 responses, but other resource types should not.
For example, the GitHub workflow API to trigger a workflow.

##### Rule: Content-Type must be used

Clients and servers rely on this header’s value to tell them how to process the sequence of bytes in a message’s body.

##### Rule: Content-Length should be used

The Content-Length header gives the size of the entity-body in bytes. In responses, this header is important for two reasons. First, a client can know whether it has read the correct number of bytes from the connection. Second, a client can make a HEAD request to find out how large the entity-body is, without downloading it.

##### Rule: Last-Modified should be used in responses

The Last-Modified header applies to response messages only. The value of this response header is a timestamp that indicates the last time that something happened to alter the representational state of the resource. Clients and cache intermediaries may rely on this header to determine the freshness of their local copies of a resource’s state representation. This header should always be supplied in response to GET requests.

##### Rule: ETag should be used in responses

##### Rule: Location must be used to specify the URI of a newly created resource

Research when to use this header.

##### Rule: Cache-Control, Expires, and Date response headers should be used to encourage caching

##### Rule: Cache-Control, Expires, and Pragma response headers may be used to discourage caching

Pragma header for legacy http 1.0

##### Rule: Caching should be encouraged

Using a small value of max-age as opposed to adding no-cache directive helps clients fetch cached copies for at least a short while without significantly impacting freshness.

##### Rule: Expiration caching headers should be used with 200 (“OK”) responses

##### Rule: Expiration caching headers may optionally be used with 3xx and 4xx responses

Known as negative caching, this helps reduce the amount of redirecting and error-triggering load on a REST API.

##### Rule: Authentication, Session, metadata, and format directives should be sent in the headers

E.g. API Keys, ClientIDs, UserIDs, JSON directive or XML directive, SessionIDs

##### Rule: Custom HTTP headers must not be used to change the behavior of HTTP methods

##### Rule: custom http headers should only be used for authentication, authorization, security, rate limiting, client preferences, feature flags, A/B testing and experimentation groups.

##### Rule: custom HTTP headers should begin with the “X-“ prefix.

##### Rule: use custom http headers only when necessary. Avoid overusing.

##### Rule: Content-Type header should always be provided

This way client knows what media type to expect.

Section: Resource Representation Design

##### Rule: JSON should be supported for resource representation

##### Rule: JSON must be well-formed

##### Rule: XML and other formats may optionally be used for resource representation through media type negotiation

##### Rule: A consistent form should be used to represent errors

E.g. {
"id" : Text,  
 "description" : Text  
}

The unique ID/code of the error type. Clients should use this ID to understand what sort of error has occurred and act/message accordingly. This can be an error code similar to Mongoose error codes thrown when there is a database transaction error. Followed by a plain text description of the error. Ideally, there should be a simple error message and a verbose error message describing the error in detail if client is displaying error to users. There should also be a link to the documentation directing users to the error code.

Rule: A consistent form should be used to represent error responses
Error responses in an API should follow a structured, predictable format to improve developer experience, debugging, and maintainability.

Client related:

##### Rule: New URIs should be used to introduce new concepts

A resource is a semantic model, like a thought about a thing.

##### Rule: Schemas should be used to manage representational form versions

Rule: Entity Tags (ETags) Should Be Used to Manage Representational State Versions
Entity Tags (ETags) are a mechanism in HTTP to track versions of a resource, helping with caching, concurrency control, and state consistency in RESTful APIs.

```plain
HTTP/1.1 200 OK
ETag: "v1.5a7d9"
Content-Type: application/json

{
  "id": 123,
  "name": "Alice",
  "email": "alice@example.com"
}
```

Rule: OAuth may be used to protect resources

Rule: API management solutions may be used to protect resources
If in house API management solution becomes overly complicated, opt-in for a 3rd-party solution.

Rule: The query component of a URI should be used to support partial responses
E.g. Excluding certain fields to get back a smaller response or to leave out unnecessary data.
E.g. Using “fields” query parameter for selected fields to be included in the response.

Rule: CORS preflight should be enabled
CORS relies on a mechanism by which browsers make a "preflight" request to the server hosting the cross-origin resource, in order to check that the server will permit the actual request.