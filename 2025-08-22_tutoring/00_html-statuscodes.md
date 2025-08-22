# HTML Statuscodes

| Code                    | Meaning                    | Typical Use                                           |
| ----------------------- | -------------------------- | ----------------------------------------------------- |
| **1xx – Informational** |                            |                                                       |
| 100                     | Continue                   | Client should continue with request                   |
| 101                     | Switching Protocols        | Protocol change (e.g. WebSocket upgrade)              |
| **2xx – Success**       |                            |                                                       |
| 200                     | OK                         | Standard success response                             |
| 201                     | Created                    | New resource successfully created                     |
| 202                     | Accepted                   | Request accepted, processing later                    |
| 204                     | No Content                 | Success, no body returned                             |
| **3xx – Redirection**   |                            |                                                       |
| 301                     | Moved Permanently          | Resource has new permanent URL                        |
| 302                     | Found (Temporary Redirect) | Old-school temporary redirect                         |
| 303                     | See Other                  | Redirects with **GET**, regardless of original method |
| 304                     | Not Modified               | Cached version is still valid                         |
| 307                     | Temporary Redirect         | Temporary, preserves method (e.g. POST stays POST)    |
| 308                     | Permanent Redirect         | Permanent, preserves method                           |
| **4xx – Client Errors** |                            |                                                       |
| 400                     | Bad Request                | Invalid request syntax/data                           |
| 401                     | Unauthorized               | Authentication required                               |
| 403                     | Forbidden                  | Authenticated but not allowed                         |
| 404                     | Not Found                  | Resource doesn’t exist                                |
| 405                     | Method Not Allowed         | E.g. POST on a GET-only route                         |
| 409                     | Conflict                   | Resource conflict (e.g. duplicate)                    |
| 429                     | Too Many Requests          | Rate limiting                                         |
| **5xx – Server Errors** |                            |                                                       |
| 500                     | Internal Server Error      | Generic server failure                                |
| 501                     | Not Implemented            | Feature not supported                                 |
| 502                     | Bad Gateway                | Invalid response from upstream server                 |
| 503                     | Service Unavailable        | Temporarily overloaded or down                        |
| 504                     | Gateway Timeout            | Upstream server took too long                         |
