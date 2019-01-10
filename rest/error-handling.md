# Error Handling

Cutwise API standard HTTP Status Codes for its responses. You can find some additional information [here](https://tools.ietf.org/html/rfc7231)

# Authentification Errors

Response for incorrect authentification requests looks like this:

```json
{"error":"invalid_client","error_description":"The client credentials are invalid"}
```

# Common Error Handling

If something goes wrong you will receive response body with following structure:

```json
{"error": ["error message", "another error message"]}
```

where `error` is array of error messages 
