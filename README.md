# mycat-download
 isCacheAble表示key是否存在于缓存之中，而不是表示是否对key进行缓存。因此，对RouteService.java的rrs.isCacheAble()进行取反操作以开启缓存模式，即：
 ```shell
 if (rrs != null && sqlType == ServerParse.SELECT && !rrs.isCacheAble()) {
			sqlRouteCache.putIfAbsent(cacheKey, rrs);
}
```
如果想关闭缓存，只需要修改配置文件cacheservice.properties的expire值为负数即可，如
```shell
#used for mycat cache service conf
factory.encache=org.opencloudb.cache.impl.EnchachePooFactory
#key is pool name ,value is type,max size, expire seconds
pool.SQLRouteCache=encache,10000,-1 #负数
pool.ER_SQL2PARENTID=encache,1000,1800
layedpool.TableID2DataNodeCache=encache,10000,1000
layedpool.TableID2DataNodeCache.TESTDB_ORDERS=50000,1800
```

建议大家采用[官网版本](https://github.com/MyCATApache/Mycat-download)