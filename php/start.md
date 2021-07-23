### PHP 学习中的知识点总结

最近在写一个推广用的博客站点，站点体量小，更新频率低，使用了PHP，在没有使用模板引擎的基础上，尽可能的优化网站的结构，模板和模块化可优化的结构，一边写一边补充PHP的知识点。



#### 模板化

针对博客的Review页和文章页优化为模板内容

+ review.php, blog.php

  + template/article.php //文章页内容部分
  + template/reviews-site.php //文章页推荐模块

  1）review.php 内容，模板化

```php+HTML
<?php session_start(); 
include_once $_SERVER['DOCUMENT_ROOT'].'/comm.php';
$article_list = array($comm[1],$comm[3]);//展示的条目
//includeTemplate 用法是为了避免模板间命名冲突
function includeTemplate ($path, $params = array()) {
    extract($GLOBALS);//引入所有全局变量
    // global $comm;//引入指定的全局变量，多重引用中，全局变量不引入，无法显示
    extract($params);
    ob_start();
    include_once $path;
    $content = ob_get_contents();
    return $content;
}
//_XML_ 名称自由定义，保证首尾一致即可。文章中变量使用花括号{}替代 
$article_content=<<<_XML_
<div class="article_title">
    <h1>{$comm[$index]['site_name']}.com Review</h1>
</div>
<p>SearchBea....</P>//省略
_XML_;
?>
<!DOCTYPE html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title><?=$comm[$index]['site_name']?>.com Review | <?=$rootsite?></title>
<?php include_once $_SERVER['DOCUMENT_ROOT'].'/screen.php';?>

</head>
<body data-name="review-page">
    
<?php include_once $_SERVER['DOCUMENT_ROOT'].'/header.php';?>
<?php includeTemplate($_SERVER['DOCUMENT_ROOT'].'/template/article.php',array(
    'content' => $article_content,
    'index' => 5,
     'reviews_sites' => array('index'=>'5'),
    ));?>

<?php include_once $_SERVER['DOCUMENT_ROOT'].'/footer.php';?>
</body>
</html>
```

​	2）article.php 文章模板

```php+HTML
<div class="container review-wrap">
    <ol class="breadcrumb">
      <li><a href="/reviews.php">Reviews</a></li>
      <li class="active"><?=$comm[$index]['site_name']?>.com Review</li>
    </ol>
    <div class="row">
        <div class="main_column col-md-8 col-sm-7 col-12">
            <div class="content_module main_content_box article">
                <?php echo $content; ?>
            </div>
        </div>
        <div class="side_column  col-lg-4 col-md-4  col-sm-5 col-12">
            <!-- 避免多文件中变量和命名冲突 -->
                <?php includeTemplate($_SERVER['DOCUMENT_ROOT'].'/reviews-sites.php');?>
        <?php //include_once $_SERVER['DOCUMENT_ROOT'].'/reviews-sites.php';?>
        </div>
    </div>
</div>
```

3） comm.php  全局变量

```php
<?php 
$comm = array(
    1 => array(
    "num"=> "1",
    "site"=> "charmmatches",
    "site_name"=> "CharmMatches",
    "site_link"=> "https://www.charmmatches.com",
    "score"=> "9.8",
    "star"=> "5.0",
    "vote"=> "14633",
    "title"=> "Top Ukrainian & Russian Dating Site",
    "overview"=> "Serious Site With Quality Russian & Ukrainian Women",
    "label"=> array(
        "0"=> "Verified Russian & Ukrainian Women",
        "1"=> "Strict Anti-Scam Policy",
        "2"=> "Welcome Chat Voucher",
    ),
    "registration"=> "FREE",
    "signup_time"=> "15 Sec",
    "monthly_user"=> "523K",
    "reply_rate"=> "95%",
    "lady_img_l"=> "",
    "lady_img_m"=> "",
    ),
    2 => array(..),
    )
 ?>
```

