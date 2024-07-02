## Postman Pre-request Script for Formatting Request Body

### Script Breakdown

```javascript
// Parse the existing raw request body into an object
const requestBody = JSON.parse(pm.request.body.raw);

// Iterate through each field in the request body
for (const key in requestBody) {
    if (requestBody.hasOwnProperty(key)) {
        // Perform any transformations or formatting here
        requestBody[key] = JSON.stringify(requestBody[key]);
    }
}

// Update the request body with the modified fields
pm.request.body.update({
    mode: "raw",
    raw: JSON.stringify(requestBody),
    options: {
        raw: {
            language: "json"
        }
    }
});
```

**Parse the Request Body:**

`const requestBody = JSON.parse(pm.request.body.raw);`

- Parses the current raw request body into a JavaScript object (`requestBody`).

**Iterate through Fields:**

`for (const key in requestBody) { ... }`

- Iterates through each field (`key`) in the `requestBody`.

**Transformation Logic:**

`requestBody[key] = JSON.stringify(requestBody[key]);`

- Converts each field value to a JSON string. You can customize this transformation logic as per your application's requirements.

**Update Request Body:**

`pm.request.body.update({ ... });`

- Updates the request body in Postman with the modified `requestBody`.

**Example Usage:**

If your initial request body is:

```json
{
    "input": "some input data",
    "otherField": 123,
    "nestedObject": {
        "nestedField": "nested value"
    }
}
```
After running the script, the request body might be transformed to:

```json
{
    "input": "\"some input data\"",
    "otherField": "\"123\"",
    "nestedObject": "{\"nestedField\":\"nested value\"}"
}
```

# Notes

- Customize the transformation logic (`JSON.stringify()`, etc.) based on the specific requirements of your server or API endpoint.
- Ensure that the transformations applied match the expected input format of your application.
- This script enables dynamic handling and formatting of all fields in the request body before sending the request, ensuring compatibility with your server's expected input structure.
