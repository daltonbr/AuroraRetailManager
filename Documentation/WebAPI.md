# WebAPI

Some apps opt to adopt a **Refresh Token** to keep extending the user log timeout, instead of having a fixed expiration time on a Token.

In Postman, we can automatically parse the token using a Test (in JavaScript).
On the snippet bellow we assume you have a variable named `token`

```js
if (pm.response.code == 200)
{
    var responseJSON = pm.response.json();
    var token = responseJSON.access_token;
    pm.environment.set('token', token);
}
```

## Two ways to handle requests

The first have a clearer return type, while the second option has a more granular control over HTTP response types (while more prone to inconsistencies in returning types).

```cs
[Authorize]
    public class ValuesController : ApiController
    {
        // GET api/values
        public IEnumerable<string> Get()
        {
            string userId = RequestContext.Principal.Identity.GetUserId();
            return new string[] { "value1", "value2", userId };
        }

        // GET api/values
        public IHttpActionResult Get()
        {
            string userId = RequestContext.Principal.Identity.GetUserId();
            return Ok(new string[] { "value1", "value2", userId });
        }
```