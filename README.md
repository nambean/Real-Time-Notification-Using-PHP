Real Time Notification Using PHP
================================

Real Time Notification on client side using PHP and Socket

How To Use
================================
Use backend.php on server side and do changes on this section

````php
<?php
  while(1) {
	$html="Hello this is real time On Server :: ".date('Y-m-d h:i:s A T');  
    echo '<script type="text/javascript">';
    echo 'comet.printServerTime("<center><b>'.$html.'</b></center>");';
    echo '</script>';
    flush(); // used to send the echoed data to the client
    usleep(10000);
    
  }
  ?>
````

You can query with database also and send to your client in place of $html

For the client side, you can do the changes on these section

````javascript

printServerTime: function (time) {
	  var oldText;
	  if(oldText!=time){
		$('content_div').innerHTML="<div class='success'>"+time+"</div>";
	  }var oldText=time;
    },
    
````

Example
================================
Lets suppose you want to show the latest comment from the database to your client
then you can do it this way.

 
````php
  $con=mysql_connect(DATABASE_HOST,DATABASE_USER,DATABASE_PASSWORD);
  $link=mysql_select_db(DATABASE_NAME);
  while(1) {
	$sql=mysql_query("select id,comment from postcomments order by id DESC");
	$lastComment=mysql_fetch_assoc($sql);
  	//$html="Hello this is real time".date('Y-m-d h:i:s');  
    echo '<script type="text/javascript">';
    echo 'comet.printServerTime("<center><b>'.$lastComment['comment'].'</b></center>");';
    echo '</script>';
    flush(); // used to send the echoed data to the client
    usleep(10000);
  }
````




