EasySNS是一个组件化平台,只需要通过开发组件你就可以轻松完成对网站的扩展.

组件的结构

组件目录位于 /application/app 下边,每个组件为一个独立目录.

![http://techblog.easysns.com/wp-content/uploads/2009/03/010.png](http://techblog.easysns.com/wp-content/uploads/2009/03/010.png)

下边我们对相关文件进行说明

operate.php 用于在安装和卸载时进行数据表操作,典型的格式如下

```
$install['sql'][] = 'CREATE TABLE IF NOT EXISTS `app_fav` (
 

`id` int(11) NOT NULL auto_increment,

PRIMARY KEY (`id`)

) ENGINE=MyISAM;';

$uninstall['table'][] = 'app_fav';
```

unction.php 放置该应用的公用函数,并在其他页面显式载入.

index.php 是访问该应用时的入口,通常是根据输入获取数据后,渲染模板.一个典型的index页面如下

```
// 载入公用函数文件
 

include_once( dirname( __FILE__ ) . '/function.php' );

// 权限检查

if( !is_login() )

{

info_page('请登录后查看');

}

// 构造数据

$data = array();

$data['ci_top_title'] = '分享';

$data['view_type'] = $view_type;

// 从url中取得一个参数

$page = array_shift( $args );

$page = intval($page) < 1 ?1:intval($page);

$limit = '10';

$start = ($page-1)*$limit;

// 数据库查询

$data['fav'] = lazy_get_data( "SELECT sql_calc_found_rows *,f.id as fid FROM `app_fav` as f LEFT JOIN `u2_user` as u ON ( f.uid = u.id ) WHERE $where ORDER BY `time` DESC LIMIT $start , $limit " );

$sql = "select found_rows()";

$all = lazy_get_var( $sql );

$base = '/app/native/ishare/index/'.$view_type;

$page_all = ceil( $all /$limit);

// 分页

$data['pager'] = get_pager( $page , $page_all , $base );

// 渲染并输出模板

layout( $data , 'default' , 'app' );
```

layout 函数将自动将$data数组中的值匹配到 view目录下的同名文件并输出.

然后我们来看微件部分.微件包含在组件的widgets目录下,每个插件独占一个目录.一般包含三个文件.

code.php为数据获取文件.一般执行数据查询操作
```
function get_system_newuser_data($para = NULL) // 函数名称的定义规则为 get_组件名_插件名_data,系统会自动调用该函数
 

{

$para = unserialize($para); // 取得插件属性,属性的变量名在稍后我们会提到的模板中定义

$limit = (isset($para['limit']) && intval( $para['limit'] ) > 0 ) ?intval( $para['limit'] ):9;

$cpl = (isset($para['cpl']) && intval( $para['cpl'] ) > 0 ) ?intval( $para['cpl'] ):3;

$data['title'] = (isset($para['title']) && strip_tags($para['title']) )!= '' ? strip_tags($para['title']):'New Members';

$CI =&get_instance();

$CI->db->select('*')->from('u2_user')->orderby('id','desc')->limit($limit);

$data['members'] = array_chunk( lazy_get_data() , $cpl );

return $data; // 返回的数据在模板中进行渲染输出
}
```

extra.fields.html用于定义首页可视化编辑时的属性设定界面 ,上文中$para数组的key值就是这里边表单元素的name值

```
<center>
<table>

<tr><td align=”left”>

<label><?=_text(’widget_title’)?>:</label>

</td><td align=”left”>

<label><INPUT TYPE=”text” NAME=”title” class=”text” value=”<? if( isset($title)){ echo $title; } ?>”></label><br clear=”all”/>

</td></tr>

<tr><td align=”left”>

<label><?=_text(’widget_show_all_number’)?>:</label>

</td><td align=”left”>

<label><INPUT TYPE=”text” NAME=”limit” class=”text” value=”<? if( isset($limit)){ echo $limit; } ?>”></label><br clear=”all”/>

</td></tr>

<tr><td align=”left”>

<label><?=_text(’widget_show_cpl_number’)?>:</label>

</td><td align=”left”>

<label><INPUT TYPE=”text” NAME=”cpl” class=”text” value=”<? if( isset($cpl)){ echo $cpl; } ?>”></label><br clear=”all”/>

</td></tr>

</table>

</center>
```

default.tph.html 是模板,用于渲染输出

```
<div class=”boxes”>
<div class=”hd”><!–{tool bar}–><?=$title;?></div> // 这里的toolbar不要删掉,模板用到的数据由code.php提供

<div class=”bd”>

<?php if($members):?>

<TABLE width=”100%”>

<?php foreach($members as $row ):?>

<TR class=”newuser_style”>

<?php foreach($row as $m ):?>

<TD valign=”top” class=”newuser_style”><div class=”warp w-normal”>

<a href=”/user/space/<?=$m['id']?>”><img src=”<?=show_user_icon(’normal’,$m['id']);?>” class=”icon” /><br/>

<strong><?=$m['u2_nickname']?></strong></a></div>

</TD>

<?php endforeach;?>

</TR>

<?php endforeach;?>

</TABLE>

<?php endif;?>

</div>

</div>
```

至此,整个EasySNS组件开发就介绍完了,总体来讲,自由度还是非常大的