
# php跨域 

在后台文件头部添加：



## 1、 允许指定的域名访问
```
header('Access-Control-Allow-Origin:http://www.xxx.com');
```
## 2、允许多个指定的域名访问
```
$origin = isset($_SERVER['HTTP_ORIGIN'])? $_SERVER['HTTP_ORIGIN'] : '';  

$allow_origin = array(  
    'http://www.guanlitnao.xyz',  
    'http://www.guanlintao.cn'
);  

if(in_array($origin, $allow_origin)){  
    header('Access-Control-Allow-Origin:'.$origin);       
}
```
## 3、允许所有访问
```
    //// 准许跨域请求。
    header("Access-Control-Allow-Origin: * ");
    header("Access-Control-Allow-Methods: POST, GET, OPTIONS, PUT, DELETE");
    /**
     * 浏览器第一次在处理复杂请求的时候会先发起OPTIONS请求。路由在处理请求的时候会导致PUT请求失败。
    * 在检测到option请求的时候就停止继续执行
    */
    if($_SERVER['REQUEST_METHOD'] == 'OPTIONS') {
        header("Access-Control-Allow-Headers: Origin, X-Requested-With, Content-Type, Accept, Authorization");
        exit;

   }
```