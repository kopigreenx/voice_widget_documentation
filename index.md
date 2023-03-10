---
layout: default
---


# Sociomile Voice widget

A widget to make outgoing call


## USAGE

#### 1. Embed widget to your application
```html
  <script>
   (function (w, d, s, o, f, js, fjs) {
        w[o] = w[o] || function () { (w[o].q = w[o].q || []).push(arguments) };
        js = d.createElement(s), fjs = d.getElementsByTagName(s)[0];
        js.id = o; js.src = f; js.async = 1; fjs.parentNode.insertBefore(js, fjs);
    }(window, document, 'script', 'socioVoice', './widget.js'));
  </script>
```

#### 2. Init widget 
##### Draggable
```html
    <script>
        socioVoice('init', { minimized: true, disableDarkMode: true ,userCredential:'credential'});
    </script>
```
##### Embed Into Element
```html
    <script>
        socioVoice('init', { element:document.querySelector('.YourUniqueElementName'),minimized: true, disableDarkMode: true ,userCredential:'credential'});
    </script>
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `element` | `boolean` | **Optional**. embed into custom element will disabled draggable feature|
| `minimized` | `boolean` | **Required**. default false (widget will expand)|
| `disableDarkMode` | `boolean` | **Required**. default false (dark mode)|
| `userCredential` | `string` | **Required**. creadential widget without credential widget not working|

#### 3. Make a call

```js
  socioVoice('event', {action:'dial',number:'08123123123',internal_id:'a12aslalsoewori',params:{}})
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `action` | `string` | **Required**. dial|
| `number` | `boolean` | **Required**. Phone number to dial|
| `internal_id` | `string` | **Required**. internal ID for sent back via webhook|
| `params` | `object` | **optional**. extra parameter for sent back via webhook|


#### 4. Extend Feature

##### Maximized widget
```js
  socioVoice('event', {action:'open'})
```

##### Minimized widget
```js
  socioVoice('event', {action:'close'})
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `action` | `string` | **Required**. open / close|




## Examples

### Direct inject to href onclick to make a call
```html
<a href="javascript:;" onclick="socioVoice('event', {action:'dial',number:'08123123123',internal_id:'internal_id'})">Call</a><br>
```
### Make a custom funtion to make a call
```html
<a href="javascript:;" onclick="dial()">to close it</a><br>
```
```js
function dial(){
    socioVoice('event', socioVoice('event', {action:'dial',number:'08123123213',internal_id:'internal_id'}))
}
```


## Webhook Response
```json
{
  "data": {
    "phone": "12312312",
    "calldate_init": "2022-11-04 13:35:51",
    "calldate_join": null,
    "calldate_end": "2022-11-04 13:35:53",
    "duration": "2",
    "duration_time": "00:00:02",
    "duration_wait": "2",
    "duration_wait_time": "00:00:02",
    "talktime": "0",
    "talktime_time": "00:00:00",
    "recordingurl": "https://link.recording",
    "disposition": "NO ANSWER",
    "uniqueid": "1667543751.398",
    "hold_sec": 0,
    "internal_id": "a12aslalsoewori",
    "extra_params": {
      "id": "asdasd",
      "req": "ttytty"
    }
  }
}
```

| Parameter | Description                |
| :-------- | :------------------------- |
|`phone` | Phone Number|
|`calldate_init` | Datetime call initiated|
|`calldate_join` | Datetime call answered by customer |
|`calldate_end` | Datetime call ended|
|`duration` | Duration call in second|
|`duration_time` | Duration call in time format|
|`duration_wait` | Duration wait in second|
|`duration_wait_time` | Duration wait in time format|
|`talktime` | Talktime call in second|
|`talktime_time` | Duration call in time format|
|`recordingurl` | URL Recording|
|`disposition` | Status Call Answered / Not Answered|
|`uniqueid` | recording trace id|
|`hold_sec` | call on hold in seconds|
|`internal_id` | internal ticket id / uniqueid value|
|`extra_params` | extra parameter |

## API Resent dan get recording
<details>
  <summary><code>POST</code> <code><b>https://app-voice.ivosights.com/api/widget/webhook/log</b></code> </summary>

##### body

> | name   |  type      | data type      | description                                          |
> |--------|------------|----------------|------------------------------------------------------|
> | `internal_id` |  required  | string         | The specific internal ID                  |
> | `resent` |  optional  | integer         | 1: resent error recording data, 0: show data                  |

##### Responses

> | http code     | content-type                      | response                                                            |
> |---------------|-----------------------------------|---------------------------------------------------------------------|
> | `200`         | `application/json`                |                                                                     |
  
  
  ```json
  [
    {
        "data": {
            "phone": "082225636817",
            "duration": "2",
            "hold_sec": 0,
            "talktime": "2",
            "uniqueid": "1678160694.1413",
            "disposition": "NO ANSWER",
            "internal_id": "a12aslalsoewori",
            "calldate_end": "2023-03-07 10:44:56",
            "extra_params": {
                "id": "asdasd",
                "req": "ttytty"
            },
            "recordingurl": "",
            "calldate_init": "2023-03-07 10:44:54",
            "calldate_join": "2023-03-07 10:44:54",
            "duration_time": "00:00:02",
            "duration_wait": "0",
            "talktime_time": "00:00:02",
            "duration_wait_time": "00:00:00"
        },
        "is_sent": 0,
        "is_error": 1,
        "messages": "Server error: `POST https://staging-crm.majoo.com/softphone/hook-callback` resulted in a `500 Internal Server Error` response:\n<!DOCTYPE html>\n<html lang=\"en\">\n<head>\n<meta charset=\"utf-8\">\n<title>Database Error</title>\n<style type=\"text/css\">\n\n:: (truncated...)\n",
        "sent_at": "2023-03-10 17:53:32"
    }
  ]
  ```



