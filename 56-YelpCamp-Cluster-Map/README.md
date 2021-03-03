# Section 56 - YelpCamp: Fancy Cluster Map

## 1. Intro To Our Cluster Map

We will add a cool cluster map onto our index page for campgrounds. It'll look like this:

![img1](https://github.com/Brian-E-Nguyen/Web-Dev-Bootcamp-2020/blob/56-YelpCamp-Cluster-Map/56-YelpCamp-Cluster-Map/img-for-notes/img1.jpg?raw=true)

Note that it may look intimidating, but we would just mostly reference code from Mapbox's documentation. There's no way that we can do this on our own

## 2. Adding Earthquake Cluster Map

**Link to the Mapbox Cluster documentation**

- https://docs.mapbox.com/mapbox-gl-js/example/cluster/

First, inside of our `campgrounds/index.ejs` file, let's make a `<div>` tag where we will place our cluster map

```html
<div id="map" style="width: 100%; height: 500px;">
    
</div>
```

Then let's copy all of the JS from that example in the link and put it inside of our new file `clusterMap.js` inside of our _public_ directory. We will then reference that file in our `campgrounds/index.ejs`

![img2](https://github.com/Brian-E-Nguyen/Web-Dev-Bootcamp-2020/blob/56-YelpCamp-Cluster-Map/56-YelpCamp-Cluster-Map/img-for-notes/img2.jpg?raw=true)

The copied JS code is using another Mapbox token. Let's use our own by referencing it inside of a `<script>` tag, just like how we did in our `campgrounds/show.ejs`

```html
<script>
    const mapToken = '<%-process.env.MAPBOX_TOKEN%>';
</script>

<script src="/js/clusterMap.js"></script>
```

## 3. Reseeding Our Database (again)

We will reseed our DB so that the campgrounds are spread out across the US. If we take a look at our _seeds_ directory and see our `cities.js` file, each city already has a latitude and longitude associated with it. Using these, we can remove the hardcoded value of `[ -122.3301, 47.6038 ]` for our coordinates and replace them with these:

```js
geometry : { 
    type : "Point", 
    coordinates : [ 
        cities[random1000].longitude,
        cities[random1000].latitude,
    ]
}
```

Now the location of the campground should be the same as what is shown on it's show page map

![img3](https://github.com/Brian-E-Nguyen/Web-Dev-Bootcamp-2020/blob/56-YelpCamp-Cluster-Map/56-YelpCamp-Cluster-Map/img-for-notes/img3.jpg?raw=true)