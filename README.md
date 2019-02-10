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

<div id="map" style="width:100%;height:400px;"></div>

<script>


function myMap() {

  //Location of Map
  var myLatLng = {lat: 34.068921, lng: -118.4473698};

//Map
  var map = new google.maps.Map(document.getElementById('map'), {
    zoom: 12,
    center: myLatLng
  });

//Star-Icon
  var pandaImage = {
    url: 'http://www.free-icons-download.net/images/cute-small-star-icon-34614.png',
    scaledSize: {
      width: 50,
      height: 50
    },
  };

  setMarkers(map);
}


function setMarkers(map) {

  var myimages = [
    ['UCLA', 'http://www.free-icons-download.net/images/cute-small-star-icon-34614.png', {lat: 34.068921, lng: -118.4473698},
        'http://my.ucla.edu', 'https://www.wallpaperup.com/uploads/wallpapers/2013/10/19/162678/a76e1c05f55d7df97fa1c5d4d218951a-700.jpg'],

    ['GETTY', 'http://cdn.shopify.com/s/files/1/1061/1924/products/Heart_Eyes_Emoji_grande.png?v=1480481053', {lat: 34.0677051, lng: -118.4670609},
        'http://www.getty.edu/', 'https://www.cesarsway.com/sites/newcesarsway/files/styles/large_article_preview/public/Natural-Dog-Law-2-To-dogs%2C-energy-is-everything.jpg?itok=Z-ujUOUr'],

    ['USC SUCKS', 'https://cdn4.iconfinder.com/data/icons/reaction/32/angry-512.png', {lat: 34.021881, lng: -118.4620083},
        'https://www.youtube.com/watch?v=gl1aHhXnN1k', 'https://www.dailynews.com/wp-content/uploads/2018/12/USC-logo-zont2.jpg?w=560']
  ];



  for (var i = 0; i < myimages.length; i++){
    var myimage = myimages[i]
    var marker = new google.maps.Marker({
      position: myimage[2],
      map: map,
      title: myimage[0],
      icon: {
        url: myimage[1],
        scaledSize: {
          width: 50,
          height: 50
        }
      }
    });

    var infowindow = new google.maps.InfoWindow();
    console.log(myimage[3]);
    const popUpBox =
      '<div>' +
        '<div> HELLO BONJOUR NIHAO ANYEONG </div>' +
        '<p> (click image for more info) </p>' +
        '<a href = ' + myimage[3] + '>' +
        '<img  width = 70%, height = 70% src = ' + myimage[4] + '/>' +
        '</a>'
      '</div>';

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
