# Sites

## List Sites

```shell
curl 'https://api.doordeck.com/site/'
  -H "Authorization: Bearer TOKEN"
```

> The above command returns JSON structured like this:

```json
[
    {
        "id": "b188b578-0035-11e8-ba89-0ed5f89f718b",
        "name": "IDEALondon",
        "logoUrl": null,
        "colour": "#666666",
        "longitude": -0.084819,
        "latitude": 51.521966,
        "radius": 20,
        "created": 1516709124.659,
        "updated": 1516709124.659
    },
    {
        "id": "7659e430-4a28-11e8-bf0b-bffab372a82e",
        "name": "Demo",
        "logoUrl": null,
        "colour": "#7AD651",
        "longitude": 0,
        "latitude": 0,
        "radius": 10,
        "created": 1524839827.955,
        "updated": 1524839827.955
    }
]
```

This endpoint lists all of the sites a user has access to.

### HTTP Request

`GET https://api.doordeck.com/site/`

## Get Locks For Site

```shell
curl 'https://api.doordeck.com/site/00000000-0000-0000-0000-000000000000/device/'
  -H "Authorization: Bearer TOKEN"
```

> Replace `00000000-0000-0000-0000-000000000000` with the site's ID.

> The above command returns JSON structured like this:

```json
[
    {
        "id": "08aa7b70-30cf-11e8-ba42-6986d3c6ca8e",
        "name": "Demo #1",
        "colour": "#1F5468",
        "start": null,
        "end": null,
        "role": "ADMIN",
        "settings": {
            "unlockTime": 7,
            "permittedAddresses": [],
            "defaultName": "Demo #1",
            "usageRequirements": {},
            "unlockBetweenWindow": null,
            "tiles": [
                "403031a2-7869-4408-9f38-c71ae51b652b"
            ]
        },
        "state": {
            "connected": true
        },
        "favourite": false
    },
    {
        "id": "49b45c50-31da-11e8-8e0f-170748b9fca8",
        "name": "Demo #2",
        "colour": "#55678C",
        "start": null,
        "end": null,
        "role": "ADMIN",
        "settings": {
            "unlockTime": 7,
            "permittedAddresses": [],
            "defaultName": "Demo #2",
            "usageRequirements": {},
            "unlockBetweenWindow": null,
            "tiles": []
        },
        "state": {
            "locked": true,
            "connected": true
        },
        "favourite": false
    }
]
```

This endpoint lists all of the locks in a particular site that the user has access to.

### HTTP Request

`GET https://api.doordeck.com/site/SITE_ID/device/`

Replace `SITE_ID` with the appropriate site ID.

## Get Users For A Site

```shell
curl 'https://api.doordeck.com/site/00000000-0000-0000-0000-000000000000/user/'
  -H "Authorization: Bearer TOKEN"
```

> Replace `00000000-0000-0000-0000-000000000000` with the site's ID.

> The above command returns JSON structured like this:

```json
[
    {
        "userId": "5b2b9930-3a7e-11e8-940e-bffab372a82e",
        "email": "michael@doordeck.com",
        "displayName": null,
        "orphan": false
    },
    {
        "userId": "f07d3ea0-593e-11e8-8257-bffab372a82e",
        "email": "john@doordeck.com",
        "displayName": null,
        "orphan": false
    }
]
```

This endpoint lists all users in the selected site, the results are filtered to ensure only locks the current user is an
administrator of will return user information.

### HTTP Request

`GET https://api.doordeck.com/site/SITE_ID/user/`

Replace `SITE_ID` with the appropriate site ID.