##用途:
在指定的函数执行前或执行后调用自己的方法,从而可以记录函数的执行时间,参数,返回值等;

..+!&#*Y^&&&/
原始作者不是我啊
我忘了跟原版相比改了哪一部分了,但是工作得挺好.
============= 我是一条无耻的分割线 ========
例子:

<pre>
function before_memcache_set($args,$result,$process_time){
    global $_VALS;
    $_VALS[]=$args;
    global $_TIME,$_COUNT;
    $_TIME["memcache_set"] += $process_time;
    $_COUNT["memcache_set"] ++;
}

function log_stat(){
    global $_TIME,$_COUNT,$_VALS;
    $f = fopen("/tmp/memcache.time.log","a+");
    fputs($f,"memcache_set:\t".$_TIME["memcache_set"]."s\t".$_COUNT["memcache_set"]." times\n");
    fputs($fp,"==================================\n");
    fclose($f);
}

fc_add_post("Memcache::set","before_memcache_set");
fc_add_post("Memcached::set","before_memcache_set");
register_shutdown_function("log_stat");

</pre>

运行时输出:

<pre>

memcache_set: 0.025305986404419s 8 times
</pre>

