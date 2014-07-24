# bdModelDB #

*Note: bdModelDB uses \LW\DB which is an mysql db framework. (https://github.com/loekwetzels) *


##Extending this class##
```php
class modelExample extends bdModelDB {
	/* Abstracts from bdModelDB */
		public function getTableName(){
			return 'table_name';
		}
		
	public function __set($getName,$getVal){
		if($getName=="something") {
			// need to do some?		
		}
		parent::__set($getName,$getVal);
	}
	
	public function yourNewFunction(){
		/* Do your own shizzle here */
		
	}
}
```

##Using this class##
- Get one object by calling it's ID
```php
$objExample = modelExample::fetchByID(1); # || fetchByPrimaryKey # returns modelExample object
```

- Get multiple objects in an array
( more functions are available example: fetchByColumn(), fetchByWhere(), etc >> check the commments in bdModelDB.php)
```php
$arrExampleObjects = modelExample::fetchAll(); #returns array(modelExample object,modelExample object,modelExample object,...)
```

- insert a new row in db, this will return a new modelExample object
```php
$objExample = modelExample::insert('My Name', 'Some Value');
```

- OR insert a new row in db with an associative array
```php
$objExample =  modelExample::insert(
	array(
		'strName' 			=> 'My Name', 
		'strSomeColumNName' => 'Some Value'
	)
);
```


- This is how you can get the db colum values
```php
$objExample->intID 				// inside the class use $this->intID
$objExample->strName 			# My Name
$objExample->strSomeColumNName  # Some Value
```

- (re) Set the vars 
```php
$objExample->strName = 'new value';
```	

- Update the database
```php
$objExample->update(); # return (boolean) on success
```

- Delete the database
```php
$objExample->delete(); # return (boolean) on success
```

- Duplicate the database
```php
	$objNew = $objExample->duplicate();
```

- getter functions
```php
$objExample->getTableName(); # table_name
$objExample->getConfigPrimaryKey(); # intID
```


- AUTO store arrays as encoded json in db
```php
# for example you have a db column called 'options' with datatype TEXT 
# when you do something like this
$objExample->options = array('a'=> 'Banana', 'b' => 'Apple');
objExample->update();

# then the value of DB colum options will be json_encoded like this:
# {"a":"Banana","b":"Apple"}
# when you call
$objExample->options 
# this value will be json_decoded again

```