---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the bashCoin API (websocket messages)
---

# Introduction

Welcome to bashCoin blockchain project. Here we share basic API message formats. Actually this is not API. Project uses Websocket message formats to exchange information. 



# Authentication

> No API-KEY required.


```python
import OpenSSL
from OpenSSL import crypto
import base64
key_file = open("key.pem", "r")
key = key_file.read()
key_file.close()
password = b'alice'

if key.startswith('-----BEGIN '):
    pkey = crypto.load_privatekey(crypto.FILETYPE_PEM, key, password)
else:
    pkey = crypto.load_pkcs12(key, password).get_privatekey()

fullMessage={"command": "getTransactionMessageForSign", "status": 0, "destinationSocket": "2", "result": {"forReciverData": "<pubKeyHashSender>:<pubKeyHashReciever>:5:3:202111121313", "forSenderData": "<pubKeyHashSender>:<pubKeyHashSender>:38:0:202111121313"}}

data=fullMessage['result']['forReciverData']+"\n"
sign = OpenSSL.crypto.sign(pkey, data, "sha256")
data_base64 = base64.b64encode(sign)
pub=base64.b64encode(pubFile)

```

```shell
# HERE WILL BE WSDUMP related
```

```javascript
NOT DEFINED
```

> No API-KEY required.

There is no special authentication mechanism for this blockchain. All data is transparent and signed by peers. We only need to generate our pub/priv key pair and sign messages to the chain. 

<aside class="notice">
no API key.
</aside>

# bashCoin

## Mine. 


```python
python wsdump.py ws://127.0.0.1:8001/
> {"command": "mine", "appType": "miner", "messageType": "direct"}
```

```shell
cd bin/
./bashCoin.sh '{"command": "mine", "appType": "miner", "messageType": "direct"}'
```

```javascript
not defined
```

> The above command returns JSON structured like this:

```json
{
  "command": "notification",
  "commandCode": "100",
  "appType": "miner",
  "messageType": "broadcast",
  "status": "0",
  "timeUTC": "20211124195158",
  "difficulty": "1",
  "MINEDBLOCK": "161.blk.solved",
  "NEXTBLOCK": "162.blk"
}
```

This endpoint retrieves json data.

### WS Request

`ws.send()`

### Query Parameters

Parameter | value | Description
--------- | ------- | -----------
command | mine | sends command name to execute bashCoin.sh
messageType | direct | means no broadcast. send directly to local app from localhost


<aside class="success">
Remember — "status":0
</aside>

## Send coin to other PubKeyHash

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves json data.


<aside class="warning">if status is not 0 means ERROR</aside>

### HTTP Request

`ws.send()`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

