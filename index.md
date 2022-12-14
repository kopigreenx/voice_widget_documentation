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



