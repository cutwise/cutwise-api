# Examples

```javascript
const USERNAME = ''; // Cutwise user login, requests will be authentificated as provided user
const PASSWORD = ''; // Cutwise user password
const CLIENT_ID = ''; // Client Application ID
const CLIENT_SECRET = ''; // Client Application Secret

fetch(`https://api-staging.cutwise.com/api/oauth/v2/token?grant_type=password&username=${USERNAME}&password=${PASSWORD}&client_id=${CLIENT_ID}&client_secret=${CLIENT_SECRET}`)
  .then(res => {
    if (!res.ok) {
      throw new Error(res.statusText);
    }

    return res;
  })
  .then(res => res.json())
  .then(authResponseAsJSON => {
    const accessToken = authResponseAsJSON.access_token;

    fetch('https://api-staging.cutwise.com/v2/constants', {
      headers: {
        Authorization: `Bearer ${accessToken}`
      }
    })
      .then(res => res.json())
      .then(constantsResponseAsJSON => {
        console.log(constantsResponseAsJSON.dict.clarity);
      });
  })
  .catch(error => console.error('Error:', error));
```
