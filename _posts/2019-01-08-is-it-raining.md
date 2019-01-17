---
layout: post
title: Is it raining in Austin right now?
featured-img:
mathjax: true
categories: [Tutorial]
---

<html>
<head>
  <script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
  <script type="text/javascript">
      $(document).ready(function(){
        if( +$("#var_text").text()>80){
          $("#responding_text").html("<i>" + " (It's totally raining!)" + "</i>");
          }
        else if (+$("#var_text").text()>40) {
          $("#responding_text").html("<i>" + " (So definitely probably.)" + "</i>" );
          }
        else if (+$("#var_text").text()>20) {
          $("#responding_text").html( "<i>" + " (So maybe?)" + "</i>");
          }
        else {
          $("#responding_text").html( "<i>" + " (So Probably not :-/ " + "</i>" );
          }
        });
  </script>
</head>

<body>

  <p>This is Karen_Bot with the weather! I'm here in Austin and there is a </p>
  <object type="text/html" id="var_text" data="https://storage.googleapis.com/is-it-raining/isitraining.txt" height="50" width="55" style="overflow:auto;border:5px ridge blue"></object><p>percent chance that it's already raining!</p>
  <p id="responding_text"></p>
  <br>
  <p>Last Update: </p>
  <object type="text/html" id="var_text" data="https://storage.googleapis.com/is-it-raining/update_date.txt" height="50" width="225"></object>

  <br>
  <a href="https://github.com/conorbarryhoke/is_it_raining">Click here for GitHub Repo</a>



</body>
</html>
