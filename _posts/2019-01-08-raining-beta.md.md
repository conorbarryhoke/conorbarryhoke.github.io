---
layout: post
title: Doing Data Science on Google Cloud
featured-img: google-cloud-setup
mathjax: true
categories: [Tutorial]
---
<!DOCTYPE html>
<html>
<head>

  <script src="https://code.jquery.com/jquery-3.2.1.min.js" type=text/javascript></script>
  <script type=text/javascript>
      $(document).ready(function(){
          $.getJSON(
              "http://35.226.182.38/",
              {format: "json"})
              .done(
                  function(data) {
                      var plot_id = data.stuff;
                      $("#retval").html( "<strong>" + plot_id + "</strong>" + " eh?" );
                  }
              );
      });
  </script>


</head>


<body>

<button>Get JSON data</button>

<div id="where">teste</div>
<div id="retval"></div>

</body>
</html>
