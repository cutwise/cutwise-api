# Examples

## Diamond API v3

This example shows authentification flow and simple requests to Cutwise API. In the following piece of code you could see Promise chain resolved with `cutShape` of the first diamond in vendor inventory. You can get additional information here:

- [Cutwise API Authentification](rest/auth.md)
- [Constants API](rest/constants-api.md)
- [Diamonds API V3](rest/diamonds-api-v3.md)

```javascript
const USERNAME = ''; // Cutwise user login, requests will be authentificated as provided user
const PASSWORD = ''; // Cutwise user password
const CLIENT_ID = ''; // Client Application ID
const CLIENT_SECRET = ''; // Client Application Secret

(async () => {
  const authResp = await fetch(`https://cutwise.com/api/oauth/v2/token?grant_type=password&username=${USERNAME}&password=${PASSWORD}&client_id=${CLIENT_ID}&client_secret=${CLIENT_SECRET}`);
  const authRespAsJSON = await authResp.json();

  if (!authResp.ok) {
    console.error(authRespAsJSON.error);
    return;
  }

  const accessToken = authRespAsJSON.access_token;
  const requestParams = {
    headers: {
      Authorization: `Bearer ${accessToken}`,
      'Content-Type': 'application/json',
    },
  };

  const constantsPromise = fetch('https://api.cutwise.com/v2/constants/web', requestParams);
  const diamondsPromise = fetch('https://api.cutwise.com/v3/diamond?limit=8&offset=0', requestParams);

  const [constantsResp, diamondsResp] = await Promise.all([constantsPromise, diamondsPromise]);
  const constantsRespAsJSON = await constantsResp.json();
  const diamondsRespAsJSON = await diamondsResp.json();

  if (!constantsResp.ok) {
    console.error(constantsRespAsJSON.error);
    return;
  }

  if (!diamondsResp.ok) {
    console.error(diamondsRespAsJSON.error);
    return;
  }

  diamondsRespAsJSON.forEach((diamond) => {
    if (!diamond.cutShape) {
      return;
    }

    const cutShape = constantsRespAsJSON.dict.cutShape.find(cs => cs.id === diamond.cutShape);

    if (!cutShape) {
      return;
    }

    console.log(cutShape);
  });
})();
```

## Diamond API v4

- [Cutwise API Authentification](rest/auth.md)
- [Diamonds API V4](rest/diamonds-api-v4.md)
- [Certifications API V4](rest/certifications-api-v4.md)

```javascript
const USERNAME = ''; // Cutwise user login, requests will be authentificated as provided user
const PASSWORD = ''; // Cutwise user password
const CLIENT_ID = ''; // Client Application ID
const CLIENT_SECRET = ''; // Client Application Secret

(async () => {
  const authRes = await fetch(`https://cutwise.com/api/oauth/v2/token?grant_type=password&username=${USERNAME}&password=${PASSWORD}&client_id=${CLIENT_ID}&client_secret=${CLIENT_SECRET}`);
  const authRespAsJSON = await authRes.json();

  if (!authRes.ok) {
    console.error(authRespAsJSON.error);
    return;
  }

  const accessToken = authRespAsJSON.access_token;
  const requestHeaders = {
    'Content-Type': 'application/json',
    Authorization: `Bearer ${accessToken}`,
  };

  const diamondResp = await fetch('https://api.cutwise.com/v4/diamond', {
    method: 'POST',
    body: JSON.stringify({
      sku: 'testqq',
      carat: 3.01,
      price: 300.0,
      isColored: false,
      isLabGrown: false,
      cutShape: 'Princess',
      clarity: 'IF',
      cutQuality: 'Fair',
    }),
    headers: requestHeaders,
  });

  const diamondAsJSON = await diamondResp.json();

  if (!diamondResp.ok) {
    console.error(diamondAsJSON.error[0]);
    return;
  }

  const certificationCreateResp = await fetch('https://api.cutwise.com/v4/certification', {
    method: 'POST',
    body: JSON.stringify({
      laboratory: 'GCAL',
      number: '33188',
      product: diamondResp.id,
    }),
    headers: requestHeaders,
  });

  const certificationCreateRespAsJSON = await certificationCreateResp.json();

  if (!certificationCreateResp.ok) {
    console.error(certificationCreateRespAsJSON.error[0]);
    return;
  }

  console.log(`Certification with id ${certificationCreateRespAsJSON.id} has been created and linked to the diamond`);
})();
```



