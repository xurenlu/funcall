从网上拷的代码，自己做了些修改的,实际上不是我写的;
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

