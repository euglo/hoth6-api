# hoth6-api

#Demo

In this demo we will be using the Google Maps API to load Google Maps into our personal website and add personalized icons and popups. 


```html
<!DOCTYPE html>
<html>
<style>
h1, h2 {
  font-family: "Comic Sans MS";
  text-align: center;
}

p {
  font-size: 70%;
}

</style>
<body>

<h1>Places to Visit in LA! :)</h1>
<h2> Using <em>Google Maps API</em> woohoo </h2>


<script>
//this function will load in our json that stores our images and the information about them
async function getIcons() {
  const response = await fetch('https://api.myjson.com/bins/17lqrk');
  const icons = await response.json();
  console.log(icons);
  return icons;
}
</script>

<div id="map" style="width:100%;height:400px;"></div>

<script>

// this function will create our map and center it at myLatLng
function myMap() {

  //Location of Map
  var myLatLng = {lat: 34.068921, lng: -118.4473698};

//Map
  var map = new google.maps.Map(document.getElementById('map'), {
    zoom: 12,
    center: myLatLng
  });

//this calls our function which is responsible for drawing our markers

  setMarkers(map);
}


//This function is reponsible for drawing our markers and making their infoWindows
async function setMarkers(map) {

  const icons = await getIcons();

  for (const myicon of icons){
    const marker = new google.maps.Marker({
      //assign the json data to each marker
      position: myicon.position,
      map: map,
      title: myicon.title,
      icon: {
        url: myicon.icon,
        scaledSize: {
          width: 50,
          height: 50
        }
      }
    });

    // This creates a pop up for when we click an icon
    var infowindow = new google.maps.InfoWindow();
    console.log(myicon);
    const popUpBox =
      '<div>' +
        '<div> HELLO BONJOUR NIHAO ANYEONG FROM ' + myicon.title +'</div>' +
        '<p> (click image for more info) </p>' +
        '<a href = ' + myicon.link + '>' +
        '<img  width = 70%, height = 70% src = ' + myicon.image + '/>' +
        '</a>'
      '</div>';

      //This adds a listener, which allows the website to know when an icon is being clicked
    google.maps.event.addListener (marker, 'click', function () {
      infowindow.setContent(popUpBox);
      infowindow.setOptions({maxWidth: 150});
       infowindow.open(map, this);
    });
  }

}
</script>

<script src="https://maps.googleapis.com/maps/api/js?key=AIzaSyBLpxRCBAV58QWZJJN6vQevrEVKd-VWhek&callback=myMap"></script>


</body>
</html>


```
