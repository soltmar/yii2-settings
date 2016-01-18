#Yii 2 Settings#

##Instalation##

###Composer###

```
composer require "marsoltys/yii2-settings:*"
```

##Configuratoion##
Add the component to the web.php config file components section:

```
#...
'settings' => [
            'class'            => 'marsoltys\yii2-settings\CmsSettings',
            'cacheComponentId' => 'cache',
            'cacheId'          => 'global_website_settings',
            'cacheTime'        => 84000,
            'tableName'        => '{{settings}}',
            'dbComponentId'    => 'db',
            'createTable'      => **true**,
            'dbEngine'         => 'InnoDB',
        ],
'cache' => [
    'class' => 'yii\caching\FileCache', // Or any other type of Cache
],
#...
```

##Usage##

```
/*   
* Set a database item:  
* $itemName can be an associative array() in key=>value pairs  ($itemValue="" in this case) 
*/
Yii::app()->settings->set($categoryName, $itemName, $itemValue, $toDatabase=true);  
 
// Get a database item:  
Yii::app()->settings->get($categoryName, $itemName);  
 
// Get all items from a category:  
Yii::app()->settings->get($categoryName);
 
// Delete a database item:  
Yii::app()->settings->delete($categoryName, $itemName);  
 
// Delete all items from a category:  
Yii::app()->settings->delete($categoryName);  
 
//Import items from a file:  
$items=include('path/to/file.php');//returns an array() in key=>value pairs  
Yii::app()->settings->set($categoryName, $items);
```

The component uses something like "lazy loading" for loading items within a category,
meaning that the items from a category will be loaded when you request them first time.
Beside this, at the end of the request, the items from that requested category are written to cache,
so next time when you request them, they will be served from cache.

Note, the component is smart enough to know itself when a new item/category has been added and refresh the cache
accordingly so you don't have to keep track of the items you add to database.

Basically, in most of the cases, the database will be hit only once, then all items will be served from cache,
which means you will get a nice way to manage the project configuration without performance penalties.