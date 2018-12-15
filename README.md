## PHP配置

### 配置设定范围
- PHP_INI_USER  
> 可以在用户脚本（ini_set）或Windows注册表以及 .user.ini

- PHP_INI_PERDIR
> 可以在 php.ini .htaccess httpd.conf

- PHP_INI_SYSTEM  
> 可以在 php.ini httpd.conf

- PHP_INI_ALL 
> 任何地方

### PHP错误级别
名称|说明|代表数字
--- | --- | ---
E_ERROR|运行时的致命错误，会中断代码执行|1
E_WARNING|警告，不影响代码执行|2
E_PARSE|编译时的语法错误|4
E_NOTICE|错误提示|8
E_CORE_ERROR|PHP初始化时的致命错误|16
E_CORE_WARNING|PHP初始化时的警告|32
E_COMPILE_ERROR|编译时的致命错误|64
E_COMPILE_WARNING|编译时的警告|128
E_USER_ERROR|用户产生的错误信息，trigger_error函数产生|256
E_USER_WARNING|用户产生的警告|512
E_USER_NOTICE|用户产生的提示|1024
E_STRICT|启用PHP对代码的修改建议|2048
E_RECOVERABLE_ERROR|可被捕获的致命错误，如果没有被自定义的catch捕捉则升级为E_ERROR|4096
E_DEPRECATED|运行时通知，启用后将在对未来版本中可能无法正常关注的代码给出警告|8192
E_USER_DEPRECATED|用户产生的警告信息|16384
E_ALL|所有错误|32767

### php.ini配置
配置名称 | 配置项 | 默认值 | 可以修改范围 | 说明
--- | --- | --- | --- | ---
engine | on off | on | A | 打开或关闭PHP解析，仅在使用PHP的Apache模块版本时才有用
short_open_tag | on off | on | A | 是否允许PHP短标签 <? ?>
precision | integer | 14 | A | 设置浮点型数据显示的有效位数
output_buffering | on off integer(bytes) | off | R | on时使用输出控制并且 buffer 无限制大小，最大字节数可 integer 指定，CLI下强制关闭
output_handler | 函数名 null | null | P | 设置将脚本所有的输出重定向到一个函数
zlib.output_compression | on off integer | off | A | 是否开启gzip压缩，开启时默认为4KB
zlib.output_compression_level | integer | -1 | A | gzip压缩级别，-1、1-9，数字越大压缩比越高，越消耗服务器性能
zlib.output_handler | string null | null | A | 作用同output_handler，但是不能同时开启
implicit_flush | on off | off | A | 开启时PHP将使输出层在每段信息块输出后自动刷新，相当于 echo后调用 flush()，CLI下强制开启
unserialize_callback_func | 函数名 null | null | A | 设置后，在反序列化时调用此函数
serialize_precision | integer | -1 | A | 控制序列化浮点数时的精度，默认保持数据不变
open_basedir | string null | null | A | 限制PHP打开文件的目录，设置后PHP只能打开设置目录下的文件，使用冒号分隔（Windows下使用分号），目录以 / 结尾
disable_functions | 函数名 ''| '' | S | 禁用函数，比如一些执行PHP脚本的函数
disable_classes | 类名 '' | '' | S | 禁止执行某些类
highlight.string |  string | '#DD0000' | A | PHP字符串语法高亮颜色配置
highlight.comment | string | '#FF8000' | A | PHP注释语法高亮颜色配置
highlight.keyword|string|'#007700'|A|PHP关键词语法高亮颜色配置
highlight.default|string|'#0000BB'|A|PHP默认文本语法高亮颜色配置
highlight.html|string|'#000000'|A|HTML语法高亮
ignore_user_abort|on off|off|A|开启时，客户端断开连接后脚本不会被终止运行
realpath_cache_size|integer|4096K|S|PHP为防止过多的include/require造成频繁去include_path中寻找路径，缓存到realpath_path
realpath_cache_ttl|integer|120|S|指定 realpath cache 过期时间，单位秒
zend.enable_gc|on off|on|A|开启或关闭垃圾回收
zend.multibyte|on off|off|P|开启或关闭多字符集编码，需要开启 mbstring
zend.script_encoding|string|null|A|开启多字符编码时的默认文件编码，优先使用declare声明的编码
expose_php|on off|on|S|是否对外暴露PHP的版本信息，开始时会在输出的header头中添加
max_executing_time|integer|30|A|设置PHP最大纸箱时间，CLI下强制为0，set_time_limit设置时，计数器会从新计时
max_input_time|integer|-1|P|脚本解析输入数据（POST、GET）允许的最大时间，单位S，默认不限制
max_input_nesting_level|integer|64|P|设置输入变量的最大深度（多少维数组），超过最大深度，该参数丢弃
max_input_vars|integer|1000|P|设置输入变量的最大个数，超过最大个数的参数被忽略
memory_limit|integer|128M|A|设置脚本运行时的最大内存，-1为不限制，小于2M时强制为2M
error_reporting|string|null|A|设置PHP报错级别，报告除 E_NOTICE以外的错误：E_ALL & ~E_NOTICE
display_errors|on off|on|A|设置是否输出错误到 stderr/stdout，会暴露服务器信息，生产环境下应该关闭
display_startup_errors|on off|off|A|设置是否输出PHP启动阶段的错误信息，生产环境下应该关闭
log_errors|on off|off|A|设置是否吧获取到的错误输出到日志文件，生产环境下建议开启
log_errors_max_len|integer|1024|A|设置错误信息的最大长度，0表示不限制
ignore_repeated_errors|on off|off|A|设置是否忽略重复的错误信息，重复信息：同一文件同一行
ignore_repeated_source|on off|off|A|设置忽略重复错误信息，也忽略信息来源，可以不说同一行代码产生的
report_memleaks|on off|on|A|设置在编译调试并且error_reporting中有E_WARNING的时候内存泄漏信息是否显示，编译调试：--enable-debug
report_zend_debug|on off|on|A|设置在编译调试时，输出zend_debug信息
track_errors|on off|off|A|开启时，会把运行时最后一个错误保存在预定义变量 $php_errormsg 中
