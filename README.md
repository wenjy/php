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

### [PHP] 配置
配置名称 | 配置项 | 默认值 | 设定范围 | 说明
--- | --- | --- | --- | ---
engine | On Off | On | A | 打开或关闭PHP解析，仅在使用PHP的Apache模块版本时才有用
short_open_tag | On Off | On | A | 是否允许PHP短标签 <? ?>
precision | integer | 14 | A | 设置浮点型数据显示的有效位数
output_buffering | On Off integer(bytes) | off | P | on时使用输出控制并且 buffer 无限制大小，最大字节数可 integer 指定，CLI下强制关闭
output_handler | 函数名 null | null | P | 设置将脚本所有的输出重定向到一个函数
zlib.output_compression | On Off integer | off | A | 是否开启gzip压缩，开启时默认为4KB
zlib.output_compression_level | integer | -1 | A | gzip压缩级别，-1、1-9，数字越大压缩比越高，越消耗服务器性能
zlib.output_handler | string null | null | A | 作用同output_handler，但是不能同时开启
implicit_flush | On Off | off | A | 开启时PHP将使输出层在每段信息块输出后自动刷新，相当于 echo后调用 flush()，CLI下强制开启
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
ignore_user_abort|On Off|Off|A|开启时，客户端断开连接后脚本不会被终止运行
realpath_cache_size|integer|4096K|S|PHP为防止过多的include/require造成频繁去include_path中寻找路径，缓存到realpath_path
realpath_cache_ttl|integer|120|S|指定 realpath cache 过期时间，单位秒
zend.enable_gc|On Off|On|A|开启或关闭垃圾回收
zend.multibyte|On Off|Off|P|开启或关闭多字符集编码，需要开启 mbstring
zend.script_encoding|string|null|A|开启多字符编码时的默认文件编码，优先使用declare声明的编码
expose_php|On Off|On|S|是否对外暴露PHP的版本信息，开始时会在输出的header头中添加
max_executing_time|integer|30|A|设置PHP最大纸箱时间，CLI下强制为0，set_time_limit设置时，计数器会从新计时
max_input_time|integer|-1|P|脚本解析输入数据（POST、GET）允许的最大时间，单位S，默认不限制
max_input_nesting_level|integer|64|P|设置输入变量的最大深度（多少维数组），超过最大深度，该参数丢弃
max_input_vars|integer|1000|P|设置输入变量的最大个数，超过最大个数的参数被忽略
memory_limit|integer|128M|A|设置脚本运行时的最大内存，-1为不限制，小于2M时强制为2M
error_reporting|string|null|A|设置PHP报错级别，报告除 E_NOTICE以外的错误：E_ALL & ~E_NOTICE
display_errors|On Off|On|A|设置是否输出错误到 stderr/stdout，会暴露服务器信息，生产环境下应该关闭
display_startup_errors|On Off|Off|A|设置是否输出PHP启动阶段的错误信息，生产环境下应该关闭
log_errors|On Off|Off|A|设置是否吧获取到的错误输出到日志文件，生产环境下建议开启
log_errors_max_len|integer|1024|A|设置错误信息的最大长度，0表示不限制
ignore_repeated_errors|On Off|Off|A|设置是否忽略重复的错误信息，重复信息：同一文件同一行
ignore_repeated_source|On Off|Off|A|设置忽略重复错误信息，也忽略信息来源，可以不说同一行代码产生的
report_memleaks|On Off|On|A|设置在编译调试并且error_reporting中有E_WARNING的时候内存泄漏信息是否显示，编译调试：--enable-debug
report_zend_debug|On Off|On|A|设置在编译调试时，输出zend_debug信息
track_errors|On Off|Off|A|开启时，会把运行时最后一个错误保存在预定义变量 $php_errormsg 中
xmlrpc_errors|On Off|Off|S|开启时，PHP输出的错误格式为XML
xmlrpc_error_number|On Off|Off|A|用做XML-RPC faultCode 元素的值
html_errors|On Off|On|A|设置是否在错误输出中启用HTML标签，关闭时输出文本格式，CLI下强制关闭
docref_root|string|''|A|设置帮助文档的地址，URL或者本地路径，html_errors开启是有效
error_prepend_string|string|null|A|设置错误信息前缀
error_append_string|string|null|A|设置错误信息后缀
error_log|string|null|A|设置错误日志保存地址，文件必须可写
arg_separator.output|string|&|A|指定PHP生成链接时的分隔符
arg_separator.input|string|&|A|指定PHP解析链接时的分隔符
variables_order|string|EGPCS|P|确定PHP注册时的超全局变量，$_ENV $_GET $_POST $_COOKIE $_SERVER
request_order|string|null|P|确定哪些超全局变量注册到 $_REQUEST 后面参数会覆盖前面同名参数
register_argc_argv|On Off|On|P|设置是否注册 $argc $argv CLI下强制开启
auto_globals_jit|On Off|On|P|设置是否延迟注册 $_ENV $_SERVER $_REQUEST，开启时将在第一次使用时创建
enable_post_data_reading|On Off|On|P|设置PHP是否会读取POST数据，关闭时 $_POST $_FILE 为空，可以通过 php:// 来读取
post_max_size|string|8M|P|设置POST提交的最大值，0表示无限制
auto_prepend_file|string|null|P|在主文件执行前自动记载执行的文件
auto_append_file|string|null|P|在主文件执行后自动记载执行的文件
default_mimetype|string|test/html|A|设置PHP输出时的默认MIME类型
default_charset|string|utf-8|A|设置PHP默认编码，header的content-type中输出的默认编码
internal_encoding|string|null|A|设置PHP内部编码，为空时，为default_charset的值
input_encoding|string|null|A|设置PHP输入编码，为空时，为default_charset的值
output_encoding|string|null|A|设置PHP输出编码，为空时，为default_charset的值
include_path|string||A|指定 require include fopen file readfile file_get_content 函数查找文件的目录列表，默认类似 .:/usr/local/php5/lib/php
odc_root|string|null|S|设置PHP运行目录，其它目录下的代码无法运行
user_dir|string|null|S|
extension_dir|string||S|动态扩展加载目录，默认类似 /usr/local/php5/lib/php/extensions/no-debug-non-zst-20160303
sys_temp_dir|string|null|S|指定PHP临时文件保存目录
enable_dl|On Off|On|S|仅对Apache有效，dl() 动态加载PHP模块
cgi.force_redirect|On Off|On|S|仅对 Apache 有效，防止通过连接直接调用PHP，此模式只会解析已经通过web服务器重定向规则的URL
cgi.nph|On Off|Off|A|开启时，CGI对每个请求都强制返回200状态码
cgi.redirect_status_env|string|null|S|cgi.force_redirect开启并且没有运行在 Apache下，需要设置一下环境变量，不建议使用
cgi.fix_pathinfo|On Off|On|S|为 CGI 提供真正的 PATH_INFO/PATH_TRANSLATED 支持
cgi.discard_path|On Off|Off|S|如果启用，PHP CGI 二进制文件可以安全的放置在web树之外，并且人们将无法规避 .htaccess 安全性
fastcgi.impersonate|On Off|Off|S|IIS 下的 FastCGI 支持模拟主叫客户端的安全令牌的能力
fastcgi.logging|On Off|On|S|使用 FastCGI 时打开 SAPI 日志记录
cgi.rfc2616_headers|On Off|A|告诉PHP发送HTTP响应代码是需要使用什么类型的标头，0表示发送web服务器支持的 Status 头，1表示符合RFC 2616
cgi.check_shebang_line|On Off|On|A|控制 CGI PHP 是否检查脚本顶部以 '#!' 开头的行
file_uploads|On Off|On|S|是否允许上传文件
upload_tmp_dir|string|null|S|文件上传的临时目录，默认使用系统指定
upload_max_filesize|string|2M|P|设置文件上传的最大值
max_file_uploads|integer|20|S|设置单个请求同时上传文件的最大数量
allow_url_fopen|On Off|On|S|设置是否允许打开远程文件（http:// ftp://）,CURL 不受此配置影响
allow_url_include|On Off|Off|S|是否允许引用远程文件，建议关闭关闭
from|string|null|A|定义匿名 FTP 的密码
user_agent|string|null|A|定义PHP发送的 User-Agent
default_socket_timeout|integer|60|A|设置 socket 流默认超时时间，单位S
auto_detect_line_endings|On Off|Off|A|开启时，检查通过fgets file 取得数据中的行结束符号是否是符合 UNIX

### [Date] 配置

### [Opcache] 配置

