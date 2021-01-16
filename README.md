## Documentation

This library is use to render google maps in your application. you will have to pass 'latLong' as a input to display google maps in your application. in case you want to add markers of your map neary by locations you will have to pass markers data as per the below defined format. when user click on any particular marker an event will execute and user will notify on which marker user has been clicked

### Installation

```sh
npm i google-maps-vue-library
```

### How we use google-maps-vue library in our applications

<GoogleMaps
      @markerClicked="clickMarkerMethod($event)"
      :markers="markers"
      :latLong="latLong"
      :apiKey="apiKey"
    />

### latLong will be input in the following format

latLong = {
    lat: your latitide,
    long: your longitude
  };

### markers will be input and data format will be as per below format

markers = [
    {
      lat: your latitude,
      long: your longitude,
      type: 'your text which will display in the marker'
    }
  ];

| Input | input purpose |
| ------ | ------ |
| apiKey: required | Your google map key, you don't need to add key in your html file |
| latLong: required | This is an object in which we will pass lat/long to display map of that particular area |
| markers: optional | we will pass as an array in case we want to display neary by markers in that particular map |

### Events

| Output | Output purpose |
| ------ | ------ |
| markerClicked | This emitter will trigger when user click on any particular marker and return that particular marker information|

### In Progress Features
Working on marker custom icons. user can pass custom icons for markers in case they don't want to display google default marker icons.

