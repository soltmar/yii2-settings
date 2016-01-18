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