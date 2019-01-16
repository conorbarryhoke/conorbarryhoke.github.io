---
layout: post
title: (this post is in beta)
featured-img:
mathjax: true
categories: [Tutorial]
---
<!DOCTYPE html>
<html>
<head>

  <script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
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

Before Retval
<div id="retval"></div>
After retval
</body>
</html>
