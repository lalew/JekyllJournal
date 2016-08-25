---
layout: post
title: PHP Cheatsheet
date:   2016-08-16
tags: [PHP, Cheatsheet]
---
Summary of Common PHP Commands/Example Files
<!-- More -->

Location of Example Files:
apache2\htdocs\BBExampleFiles

[Cheat Sheet](https://www.cheatography.com/davechild/cheat-sheets/php/)

**PHP 'echo' and 'print' Statements**

echo and print are more or less the same. They are both used to output data to the screen.

The differences are small: echo has no return value while print has a return value of 1 so it can be used in expressions. echo can take multiple parameters (although such usage is rare) while print can take one argument. echo is marginally faster than print, which is why it is most commonly used.


**Comment DocBlock example**
{% highlight php %}
/**
  * A summary of this PHP Basics course on Treehouse.
  *
  * A *description*, that can span multiple lines, to go _in-depth_ into the details of this 
  *  element and to provide some background information or textual references.
  *
  * @source Author
  * 
  * @param string $myArgument With a *description* of this argument, these may also
  *    span multiple lines.
  *
  * @return type (a PHP Programmer ;) )
  */
{% endhighlight %}

Summary A short piece of text, usually one line, providing the basic function of the associated element.

Description An optional longer piece of text providing more details on the associated element’s function. This is very useful when working with a complex element.

A series of tags These provide additional information in a structured manner. With these tags you can link to other elements, provide type information for properties and arguments, and more.

$score = 0;

PHP supports eight primitive types.

Four scalar types:
-boolean
-integer
-float (floating-point number, aka double)
-string
Two compound types:
-array
-object
And finally two special types:
-resource
-NULL

**DocBlock**
{% highlight php %}
     /**
      * This method sets a description.
      *
      * @param string $description A text with a maximum of 80 characters.
      *
      * @return void
      */
     public function setDescription($description)
     {
         // there should be no docblock here
         $this->description = $description;
     }

is_bool()
var_dump(<variable>) - type and value contained
{% endhighlight %}

PHP-FIG - PHP Unofficial Standards
PHP Framework Interop Group
http://www.php-fig.org/

http://php.net/manual/en/function.date.php
date('<param>');

You can place copyright in footer
{% highlight php %}
<?php
$displayName = "Placeholder Name";
?>
<?php echo "Last modified: " . date ("F d Y H:i:s.", getlastmod()); ?>
{% endhighlight %}

```php
<!DOCTYPE html>

Array Print Separated by a Delimiter
echo implode("\n",$learn);

Array
$learn = array('firstarr','secarr','thirdArr');
$learn[] = 'Testing";
array_push($learn,'arg1','arg2');

// 1-based array (instead of traditional 0-based)
$array = array(1 => 1, 1, 1, 1,  1, 8 => 1,  4 => 1, 19, 3 => 13);
print_r($array);


<?php
$learn = array('firstarr','secarr','thirdArr');
$learn[] = 'Testing';
array_push($learn,'arg1','insertEnd');

var_dump($learn);

echo "\n\n";

array_unshift($learn,'insertBegin');

unset($learn[3],$learn[4]);
$firstElem = array_shift($learn);
$lastElem = array_pop($learn);

var_dump($learn);
echo $learn[1];


//echo implode("\n",$learn);

?>
```

Associative array
<?php
$iceCream = array('Name1' => "Flavor1", 'Name2' => "Flavor2");
echo $iceCream['Name1'];
// Same but without "array" keyword
// $iceCream = ['Name1' => "Flavor1", 'Name2' => "Flavor2"];


// Now, $Name1 = "Flavor1" and $Name2 likewise
extract($iceCream);

echo $Name1;

?>

Multi-dimensional arrays

```php
$contacts = array(array('name' => 'Alena Holligan',
                       'email' => 'alena.holligan@teamtreehouse.com'), 
                  array('name' => 'Dave McFarland',
                       'email' => 'dave.mcfarland@teamtreehouse.com'), 
                  array('name' => 'Treasure Porth',
                       'email' => 'treasure.porth@teamtreehouse.com'), 
                  array('name' => 'Andrew Chalkley',
                       'email' => 'andrew.chalkley@teamtreehouse.com'));

// HTML with PHP Code - Tags are quoted - Accessing Multi-dim
echo "<li>".$contacts[0]['name']." : ".$contacts[0]['email']."</li>\n";

Sorts
//All sorts do not return a sorted array
sort, asort, ksort, rsort
sort - reindexes

For Each
while ((list($key, $val) = each($todo)) && (++$count <= 2)) {
    echo "$key => $val\n";
}

Checks if Key exists, then if key is not null
Both return false if key is not in the array at all.
isset @return false if value is null or empty
array_key_exists @return true if value is null or empty
<?php 
if (isset($Arr['MyElement']) || array_key_exists('MyElement', $Arr)) { 
      ... do my stuff ... 
} ?>


rand(0,1)
for ($letter = ord("A"); $letter <= ord("Z"); $letter++)
{
    echo chr($letter) . ", ";
}


For Each Loop
<?php
// Pull in $list[]
include 'list.php';

// All includes completed tasks (Usually ignored)
// Status = true/false/'all'
$status = 'all';
// Field is one of the keys
$field = 'priority';
$action = 'week';

// Blank array to place keys in later. Where key is title, priority, etc.
$order = array();

if ($status == 'all') {
  echo "We are not filtering by completed/incomplete<br>";
  $order = array_keys($list);
} else {

  foreach ($list as $key => $item) {
    // 'all', true, or false items
    if ($item['complete'] == $status) {
      $order[] = $key;
      echo "item['complete'] == status";
    }
  }
}

switch($action) {
  case 'sort':
    echo "Executing switch-case statement 'sort'<br>";
    // Sort by field type: priority, due date, title, etc.
    if ($field) {
      $sort = array();
      // Order is each todo task: ArrayIndex, laundry, etc.
      foreach ($order as $id) {
        // sort[key] = list[arrayIndex][key];
        $sort[$id] = $list[$id][$field];
      }
      asort($sort);
      $order = array_keys($sort);
    }
    break;
  case 'week':
    echo "Executing switch-case statement 'week'<br>";
    foreach ($order as $key => $value) {
      if (strtotime($list[$value]['due']) > strtotime("+1 week")) {
        unset($order[$key]);
      }
    }
    break;
}
```

// So we have the sorted arrray keys now
// Ex: 
// OriginalIndices: 0,1,2,3
// SortedIndices:   2,3,0,1   //This is preserved in $order
```php
echo '<table>';
echo '<tr><th>Title</th>';
echo '<th>Priority</th>';
echo '<th>Due Date</th>';
echo '<th>Complete</th>';
echo '</tr>';
foreach($order as $id) {
  echo '<tr>';
  echo '<td>'.$list[$id]['title']    . "</td>\n";
  echo '<td>'.$list[$id]['priority'] . "</td>\n";
  echo '<td>'.$list[$id]['due']      . "</td>\n";
  echo '<td>';
  
  if($list[$id]['complete']) {
    echo 'Yes';
  } else {
    echo 'No';
  }
    
  echo "</td>\n";
  echo '</tr>';
  
}
echo '</table>';
//var_dump($list);



?>
```

// If you need to associate a key with a val
foreach ($arr1 as $key => &$val) {}


// Performance of different foreach
foreach(array_keys($arr) as $key)
Is about 50% to 60% slower in comparison to
foreach($arr as $key => $notUsed)

// Two ways to pull keys OR keys and value from array
$parameters = array(
  "day" => 1,
  "month" => 8,
  "year" => 2010
);
foreach($parameters as $paramName => $paramValue)
  echo $paramName . "<br>";
foreach(array_keys($parameters) as $paramName)
  echo $paramName . "<br>";

// Array_keys - Find key that value is associated with -
array_keys(array,value,strict)

//foreach loop example
{% highlight php %}
<?php

$flavors = array();
$flavors[] = array("name" => "Cookie Dough",      "in_stock" => true);
$flavors[] = array("name" => "Vanilla",           "in_stock" => false);
$flavors[] = array("name" => "Avocado Chocolate", "in_stock" => false);
$flavors[] = array("name" => "Bacon Me Crazy",    "in_stock" => true);
$flavors[] = array("name" => "Strawberry",        "in_stock" => false);

//add your code below this line
$resArr=array();
foreach ($flavors as $key => $value) {
  
  //Each key is an "array" with name and in_stock attribute
  if ($value["in_stock"] == true)
    echo $value["name"];
}
?>
{% endhighlight %}

First Created: 8/16/16
Last Modified: 8/18/16