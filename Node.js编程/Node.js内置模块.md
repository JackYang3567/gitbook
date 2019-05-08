# Node.js内置模块

## 1、URL模块

URL模块，一共提供了三个方法，分别是url.format();  url.parse();　url.resolve();  

### 1.0、URL模块使用
先在程序顶部导入
```
const url = require('url');
```
### 1.1、url.format(urlObject)方法
url.format(urlObject) 方法返回一个从 urlObject 格式化后的 URL 字符串。  
参数 urlObject 应是一个对象，否则报错。

```
url.format({
    protocol:"http:",
    hostname:"192.168.33.10",
    port:"8080"
});
/*
返回值：
'http://192.168.33.10:8080'
*/
```
### 1.2、url.parse(urlString)方法
解析 URL 字符串并返回 URL 对象。  
如果 urlString 不是字符串，则抛出TypeError。  
如果 auth 属性存在但无法解码，则抛出 URIError。  

```
const urlString = "https://live.leisu.com/"
const Url = url.parse(urlString)

输出：
Url {
  protocol: 'https:',
  slashes: true,
  auth: null,
  host: 'live.leisu.com',
  port: null,
  hostname: 'live.leisu.com',
  hash: null,
  search: null,
  query: null,
  pathname: '/',
  path: '/',
  href: 'https://live.leisu.com/' 
}
```
### 1.3、url.resolve(from, to)方法
**from** &lt;string&gt; 解析时相对的基本 URL。  
**to** &lt;string&gt; 要解析的超链接 URL。  
url.resolve() 方法会以一种 Web 浏览器解析超链接的方式把一个目标 URL 解析成相对于一个基础 URL。
```
const url = require('url');
url.resolve('/one/two/three', 'four');         // '/one/two/four'
url.resolve('http://example.com/', '/one');    // 'http://example.com/one'
url.resolve('http://example.com/one', '/two'); // 'http://example.com/two'
```

## 2、path - 路径 模块
path 模块提供用于处理文件路径和目录路径的实用工具。 

### 2.0、path模块使用
先在程序顶部导入：  
```
const path = require('path');
```
path - 路径 模块提供的方法
### 2.1、path.basename(path[, ext])
**path** &lt;string&gt;  
**ext** &lt;string&gt; 可选的文件扩展名。  
返回: &lt;string&gt;  

path.basename() 方法返回 path 的最后一部分(文件名)，类似于 Unix 的 basename 命令。 尾部的目录分隔符将被忽略

```
path.basename('/foo/bar/baz/asdf/quux.html');
// 返回: 'quux.html'

path.basename('/foo/bar/baz/asdf/quux.html', '.html');
// 返回: 'quux'
```
### 2.2、path.dirname(path)
path  &lt;string&gt;   
返回:  &lt;string&gt;   
path.dirname() 方法返回 path 的目录名，类似于 Unix 的 dirname 命令。 尾部的目录分隔符将被忽略```

```
path.dirname('/foo/bar/baz/asdf/quux');
// 返回: '/foo/bar/baz/asdf'
```
### 2.3、path.extname(path)
path &lt;string&gt;   
返回: &lt;string&gt;  
path.extname() 方法返回 path 的扩展名，从最后一次出现 .（句点）字符到 path 最后一部分的字符串结束。 如果在 path 的最后一部分中没有 . ，或者如果 path 的基本名称的第一个字符是 .，则返回空字符串。  

```
path.extname('index.html');
// 返回: '.html'

path.extname('index.coffee.md');
// 返回: '.md'

path.extname('index.');
// 返回: '.'

path.extname('index');
// 返回: ''

path.extname('.index');
// 返回: ''
```

### 2.4、path.format(pathObject)
```
pathObject = {  
  dir  <string>  
  root  <string>   
  base  <string>  
  name  <string>  
  ext  <string>  
}
```
返回: &lt;string&gt;   
path.format() 方法从对象返回路径字符串。 与 path.parse() 相反。  
当为 pathObject 提供属性时，注意以下组合，其中一些属性优先于另一些属性：  

如果提供了 pathObject.dir，则忽略 pathObject.root。  
如果 pathObject.base 存在，则忽略 pathObject.ext 和 pathObject.name。  
例如，在 POSIX 上：

```
// 如果提供了 `dir`、 `root` 和 `base`，
// 则返回 `${dir}${path.sep}${base}`。
// `root` 会被忽略。
path.format({
  root: '/ignored',
  dir: '/home/user/dir',
  base: 'file.txt'
});
// 返回: '/home/user/dir/file.txt'

// 如果未指定 `dir`，则使用 `root`。 
// 如果只提供 `root`，或 'dir` 等于 `root`，则将不包括平台分隔符。 
// `ext` 将被忽略。
path.format({
  root: '/',
  base: 'file.txt',
  ext: 'ignored'
});
// 返回: '/file.txt'

// 如果未指定 `base`，则使用 `name` + `ext`。
path.format({
  root: '/',
  name: 'file',
  ext: '.txt'
});
// 返回: '/file.txt'
```
在 Windows 上：
```
path.format({
  dir: 'C:\\path\\dir',
  base: 'file.txt'
});
// 返回: 'C:\\path\\dir\\file.txt'

```
### 2.5、path.join([...paths])

...paths &lt;string&gt;    路径片段的序列。  
返回: &lt;string&gt;  
path.join() 方法使用平台特定的分隔符作为定界符将所有给定的 path 片段连接在一起，然后规范化生成的路径。  

零长度的 path 片段会被忽略。 如果连接的路径字符串是零长度的字符串，则返回 '.'，表示当前工作目录。

```
path.join('/foo', 'bar', 'baz/asdf', 'quux');
// 返回: '/foo/bar/baz/asdf/quux'

path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');
// 返回: '/foo/bar/baz/asdf'

```
### 2.6、path.parse(path)

path &lt;string&gt;  
返回: &lt;Object&gt;  
path.parse() 方法返回一个对象，其属性表示 path 的重要元素。 尾部的目录分隔符将被忽略。  
返回的对象将具有以下属性：  

dir &lt;string&gt;
root &lt;string&gt;
base &lt;string&gt;
name &lt;string&gt;
ext &lt;string&gt;

例如，在 POSIX 上：
```
path.parse('/home/user/dir/file.txt');
// 返回:
// { root: '/',
//   dir: '/home/user/dir',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file' }
```

### 2.7、path.resolve([...paths])
...paths &lt;string&gt; 路径或路径片段的序列。  
返回: &lt;string&gt;  
path.resolve() 方法将路径或路径片段的序列解析为绝对路径。  

给定的路径序列从右到左进行处理，每个后续的 path 前置，直到构造出一个绝对路径。 例如，给定的路径片段序列：/foo、 /bar、 baz，调用 path.resolve('/foo', '/bar', 'baz') 将返回 /bar/baz。  

如果在处理完所有给定的 path 片段之后还未生成绝对路径，则再加上当前工作目录。  

生成的路径已规范化，并且除非将路径解析为根目录，否则将删除尾部斜杠。  

零长度的 path 片段会被忽略。  

如果没有传入 path 片段，则 path.resolve() 将返回当前工作目录的绝对路径。  

```
path.resolve('/foo/bar', './baz');
// 返回: '/foo/bar/baz'

path.resolve('/foo/bar', '/tmp/file/');
// 返回: '/tmp/file'

path.resolve('wwwroot', 'static_files/png/', '../gif/image.gif');
// 如果当前工作目录是 /home/myself/node，
// 则返回 '/home/myself/node/wwwroot/static_files/gif/image.gif'
```



