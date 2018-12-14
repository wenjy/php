## 配置设定范围
PHP_INI_USER  可以在用户脚本（ini_set）或Windows注册表以及 .user.ini
PHP_INI_PERDIE  可以在 php.ini .htaccess httpd.conf
PHP_INI_SYSTEM  可以在 php.ini httpd.conf
PHP_INI_ALL 任何地方

### [PHP]相关设置

配置名称 | 配置项 | 默认值 | 可以修改范围 | 说明

--- | --- | --- | --- | ---

engine | on off | on | A | 打开或关闭PHP解析，仅在使用PHP的Apache模块版本时才有用

short_open_tag  on|off  on  A 是否允许PHP短标签 <? ?>
precision integer 14  A 设置浮点型数据显示的有效位数
output_buffering  on|off|integer(bytes) R on时使用输出控制并且 buffer 无限制大小，最大字节数可 integer 指定，CLI下强制关闭
output_handler  函数名|null  null  P 设置将脚本所有的输出重定向到一个函数
zlib.output_compression on|off|integer  off A 是否开启gzip压缩，开启时默认为4KB
zlib.output_compression_level integer -1  A gzip压缩级别，-1、1-9，数字越大压缩比越高，越消耗服务器性能
zlib.output_handler string|null  null A 作用同output_handler，但是不能同时开启
implicit_flush  on|off  off A 开启时PHP将使输出层在每段信息块输出后自动刷新，相当于 echo后调用 flush()，CLI下强制开启
unserialize_callback_func 函数名|null null  A 设置后，在反序列化时调用此函数
serialize_precision integer -1  A 控制序列化浮点数时的精度，默认保持数据不变
open_basedir  string|null null  A 限制PHP打开文件的目录，设置后PHP只能打开设置目录下的文件，使用冒号分隔（Windows下使用分号），目录以 / 结尾
disable_functions 函数名|'' '' S 禁用函数，比如一些执行PHP脚本的函数
disable_classes 类名|'' '' S  禁止执行某些类
highlight.string  string  '#DD0000' A PHP字符串语法高亮颜色配置
highlight.comment string  '#FF8000' A PHP注释语法高亮颜色配置
