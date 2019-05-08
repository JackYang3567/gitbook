# PHP编程
## Yii

### 1、Composer
> Composer是 PHP 用来管理依赖（dependency）关系的工具。你可以在自己的项目中声明所依赖的外部工具库（libraries），Composer 会帮你安装这些依赖的库文件。  

#### 1.1、Composer简介
> Composer 不是一个包管理器。是的，它涉及 "packages" 和 "libraries"，但它在每个项目的基础上进行管理，在你项目的某个目录中（例如 vendor）进行安装。默认情况下它不会在全局安装任何东西。因此，这仅仅是一个依赖管理。

#### 1.2、Composer安装 - *nix
##### 1.2.1、全局安装
你可以将此文件放在任何地方。如果你把它放在系统的 PATH 目录中，你就能在全局访问它。 在类Unix系统中，你甚至可以在使用时不加 php 前缀。  

你可以执行这些命令让 composer 在你的系统中进行全局调用：  

```
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
```
#### 1.3、Composer使用
##### 1.3.1、Composer安装 Yii
安装 Composer 后，您可以通过在 Web 可访问的文件夹下运行以下命令来 安装Yii应用程序模板：

```
cd /www/wwwroot/dev.yiiphp.com/
composer create-project --prefer-dist yiisoft/yii2-app-basic basic
```