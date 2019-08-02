# First Group Project

The purpose of this project was to create a simple multi-page website as a group, utilzing Github to share and manage our files. This group project served as a training ground for learning about Git workflows. It is intended to be incomplete and will likely not be updated. While using a branch workflow is what we initially set out to do, we decided on merging our branches to the master a bit earlier in order for all of our teammates to keep track of the individual parts of the project. In summary, it was a success. Personally, I overcame an issue I had with CSS involving align-items. Using the browser developer tools in Google Chrome was instrumental in correcting it. Also, the site was built using Bootstrap. 

## Collaborators

* [Oshea Deans](https://github.com/OsheaRD)
* [Terrence Eveline](https://github.com/tjeve)
* [Joey Killam](https://github.com/jhkillam)
* [Kazue Sasatani](https://github.com/segakazzz)

## Key Takeaways

Github proved to be a very useful tool for us to share what we were working on, and to help each other out with any issues. If I had more time to work on this with the group, I would have liked to clean up the file structure, and also merged all of our css files into one master stylesheet, rather than using stylesheets for each page. Additionally, I would have liked to put more content into the footer to be used across the rest of the site.

## Subscribe-Page

### Designed by [Terrence Eveline](https://github.com/tjeve)

# This is our project!

## Testimonies

* Used JQuery Plugin [Masonry](https://masonry.desandro.com/) for Masonry layout to avoid adjusting the ratio of width and height for each photo.

~~~html
<script src="https://unpkg.com/masonry-layout@4/dist/masonry.pkgd.min.js"></script>
~~~

~~~js
  let masonry = function() {
    $(".grid").masonry({
      // options
      itemSelector: ".grid-item",
      columnWidth: 400,
      fitWidth: true
    });
  };
  masonry();
~~~

* [Bootstrap Cards](https://getbootstrap.com/docs/4.0/components/card/) is used for card layout

~~~html
<div class="testimony grid-item>
  <div class="card"><img src="img/amalfi.jpg" class="card-img-top">
    <div class="card-body">
      <h5><span class="badge badge-danger">New!</span>Amalfi Coast</h5>
      <p>The Amalfi Coast (Italian: Costiera Amalfitana) is a stretch of coastline on the northern coast of the Salerno Gulf on the Tyrrhenian Sea, located in the Province of Salerno of southern Italy.</p>
      <div class="container-fluid location"><i class="fas fa-thumbtack"></i>Amalfi, Italy</div>
      <hr>
      <div class="container-fluid comment-area">
        <div class="row">
          <div class="face col-3"><img src="./img/KazuePic.jpeg"></div>
          <div class="comment col">Beautiful, beautiful and beautiful....</div>
        </div>
        <div class="row">
          <div class="date col-12">Jul 2, 2019</div>
        </div>
      </div>
    </div>
  </div>
</div>
~~~

* Jquery code in [js/testimonies.js](js/testimonies.js) creates the dom of card elements by loading [testimonies.json](testimonies.json). This is to avoid to write complecatedly nested html cards.

~~~json
  {
    "imgSource": "img/amalfi.jpg",
    "date": "2019-07-02",
    "city": "Amalfi",
    "country": "Italy",
    "title": "Amalfi Coast",
    "text": "The Amalfi Coast (Italian: Costiera Amalfitana) is a stretch of coastline on the northern coast of the Salerno Gulf on the Tyrrhenian Sea, located in the Province of Salerno of southern Italy.",
    "who": "Kazue",
    "comment": "Beautiful, beautiful and beautiful...."
  }
~~~

* On refreshing the page, the order of cards is shuffled by Javascript code.

~~~js
    for (var i = data.length - 1; i > 0; i--) {
      var r = Math.floor(Math.random() * (i + 1));
      var tmp = data[i];
      data[i] = data[r];
      data[r] = tmp;
    }
~~~    

* On clicking each card, the size of photo is toggled between small(400px in width) and large (800px in width). The masonry layout is re-generated on click action.

~~~js
    $(".testimony.grid-item").on("click", function() {
      let size = $(this).hasClass("large") ? { width: 800 } : { width: 400 };
      $(this)
        .toggleClass("large")
        .animate(size, masonry);
    });
~~~

* [Bootstrap Badges](https://getbootstrap.com/docs/4.3/components/badge/) is used for showing "New" for images added recently (within a month). This is automatically judged by looking "date" key in json data. 

~~~js
    let newAfter = new Date();
    newAfter.setMonth(-1);
    let date = new Date(element.date);
    let isNew = newAfter < date;
    let $new = $("<span>")
        .addClass("badge badge-danger")
        .text("New!");
    let $cardTitle = $("<h5>").text(element.title);
    if (isNew) {
        $cardTitle.prepend($new);
    }
~~~
