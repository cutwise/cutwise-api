## Example

This example shows authentification flow and simple requests to Cutwise API. In the following piece of code you could see Promise chain resolved with `cutShape` of the first diamond in vendor inventory. You can get additional information here:

- [Cutwise API Authentification](rest/auth.md)
- [Constants API](rest/constants-api.md)
- [Diamonds API](rest/diamonds-api.md)

```javascript
const USERNAME = ''; // Cutwise user login, requests will be authentificated as provided user
const PASSWORD = ''; // Cutwise user password
const CLIENT_ID = ''; // Client Application ID
const CLIENT_SECRET = ''; // Client Application Secret

fetch(`https://api.cutwise.com/api/oauth/v2/token?grant_type=password&username=${USERNAME}&password=${PASSWORD}&client_id=${CLIENT_ID}&client_secret=${CLIENT_SECRET}`)
  .then(res => {
    if (!res.ok) {
      throw new Error(res.statusText);
    }

    return res;
  })
  .then(res => res.json())
  .then(authResponseAsJSON => {
    const accessToken = authResponseAsJSON.access_token;

    const constantsPromise = fetch('https://api.cutwise.com/v2/constants', {
      headers: {
        Authorization: `Bearer ${accessToken}`
      }
    }).then(res => res.json());

    const diamondsPromise = fetch('https://api.cutwise.com/v3/diamond?limit=8&offset=0', {
      headers: {
        Authorization: `Bearer ${accessToken}`
      }
    }).then(res => res.json());

    return Promise.all([constantsPromise, diamondsPromise]).then(([constants, diamonds]) => {
      diamonds.forEach((diamond) => {
        if (!diamond.cutShape) {
          return;
        }

        const cutShape = constants.dict.cutShape.find(cutShape => cutShape.id === diamond.cutShape);

        if (!cutShape) {
          return;
        }

        console.log(cutShape);
        
        return cutShape;
      });
    });
  })
  .catch(error => console.error('Error:', error));
```
