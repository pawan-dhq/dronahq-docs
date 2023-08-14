---
sidebar_position: 7
---

# Retrieve a Group

Retrieve a Group by ID.

<div class="apidocs-header">
    <div class="method get">GET</div>
    <div class="endpoint">/api/scim/v2/Groups/&#123;id&#125;</div>
</div>


#### Headers
<table>
    <tr>
        <th>Key</th>
        <th>Value</th>
    </tr>
    <tr>
        <td>Accept</td>
        <td>application/json</td>
    </tr>
    <tr>
        <td>Authorization</td>
        <td>Bearer &lt;API Token&gt;</td>
    </tr>
</table>

#### Path Parameter

- `id` (required): Group ID to retrieve the specific group.

#### Example cURL

```bash
curl --location 'http://localhost:8080/api/scim/v2/Groups/group-123' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX'
```
#### Responses
<table>
    <tr>
        <th>Status Code</th>
        <th>Description</th>
        <th>Response</th>
    </tr>
    <tr>
        <td>200</td>
        <td>Group retrieved successfully</td>
        <td>application/json</td>
    </tr>
    <tr>
        <td>400</td>
        <td>Invalid Request</td>
        <td>empty</td>
    </tr>
    <tr>
        <td>401</td>
        <td>Unauthorized</td>
        <td>empty</td>
    </tr>
    <tr>
        <td>500</td>
        <td>Internal Server Error</td>
        <td>empty</td>
    </tr>
</table>

#### Sample response
200 : Group retrieved successfully

```json
{
    "id": "123",
    "displayName": "Developers",
    "members": [
        {
            "value": 1,
            "display": "user1@example.com"
        },
        {
            "value": 2,
            "display": "user2@example.com"
        }
    ],
    "meta": {
        "location": "http://localhost:8080/api/scim/v2/Groups/group-123",
        "created": "2023-08-04T08:38:02.3732123Z"
    }
}
```