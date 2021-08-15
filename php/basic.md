### 将PHP数组转换为Javascript数组

一边使用一边学习PHP的基础知识记录

要点： json_encode()函数。

##### 一维索引数组

下面的示例将数字索引的PHP数组转换为JavaScript数组。

**PHP**
```php
//PHP
$userArray = array('John Doe', 'john@example.com');
```
**JavaScript**
```JavaScript
//JavaScript:

var users = <?php echo json_encode($userArray); ?>;
```

在JavaScript中访问数组元素：
```
alert(users[0]); //output will be "John Doe"
```


##### 多维索引数组
下面的示例将数字索引的PHP多维数组转换为JavaScript数组。

**PHP**
```php
//PHP
$userArray = array(
    array('John Doe', 'john@example.com'),
    array('Marry Moe', 'marry@example.com'),
    array('Smith Watson', 'smith@example.com')
);
```
**JavaScript**

```JavaScript

var users = <?php echo json_encode($userArray); ?>;
```
在JavaScript中访问数组元素：
```JavaScript
alert(users[1][0]); //output will be "Marry Moe"
```

##### 多维关联数组
下面的示例将关联的PHP多维数组转换为JavaScript数组。
**PHP**
```php
//PHP
$userArray = array(
    array('name'=>'John Doe', 'email'=>'john@example.com'),
    array('name'=>'Marry Moe', 'email'=>'marry@example.com'),
    array('name'=>'Smith Watson', 'email'=>'smith@example.com')
);
```
**JavaScript**
```javascript

var users = <?php echo json_encode($userArray); ?>;
```
在JavaScript中访问数组元素：
```javascript
alert(users[0].email); //output will be "john@example.com"
```
