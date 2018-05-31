# Tiles

## Get Lock Belonging To Tile

```shell
curl 'https://api.doordeck.com/tile/00000000-0000-0000-0000-000000000000/'
  -H "Authorization: Bearer TOKEN"
```

> Replace `00000000-0000-0000-0000-000000000000` with the tile ID.

> The above command returns 404 if no tile is known, or a see other 303 with the `Location` header set to the value of 
the lock

This endpoint identifies which lock belongs to the specific tile.

### HTTP Request

`GET https://api.doordeck.com/tile/TILE_ID/`

Replace `TILE_ID` with the appropriate tile ID.

## Associate Tile With Lock

```shell
curl 'https://api.doordeck.com/device/00000000-0000-0000-0000-000000000000/tile/00000000-0000-0000-0000-000000000001'
  -X PUT
  -H "Authorization: Bearer TOKEN"
```

> Replace `00000000-0000-0000-0000-000000000000` with the device ID.

> Replace `00000000-0000-0000-0000-000000000001` with the tile ID.

The endpoints links a tile to a lock; the current user must be an administrator of the lock and the tile must not be 
associated to any other locks.

### HTTP Request

`PUT https://api.doordeck.com/device/DEVICE_ID/tile/TILE_ID/`

Replace `TILE_ID` with the appropriate tile ID and `DEVICE_ID` with the appropriate device ID.

## Disassociate Tile From Lock

```shell
curl 'https://api.doordeck.com/device/00000000-0000-0000-0000-000000000000/tile/00000000-0000-0000-0000-000000000001'
  -X DELETE
  -H "Authorization: Bearer TOKEN"
```

> Replace `00000000-0000-0000-0000-000000000000` with the device ID.

> Replace `00000000-0000-0000-0000-000000000001` with the tile ID.

The endpoint removes the relationship between a tile and a lock, the tile can then be reassigned to another lock.

### HTTP Request

`DELETE https://api.doordeck.com/device/DEVICE_ID/tile/TILE_ID/`

Replace `TILE_ID` with the appropriate tile ID and `DEVICE_ID` with the appropriate device ID.