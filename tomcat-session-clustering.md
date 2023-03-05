## 아파치 + 톰캣 구성에서의 세션 클러스터링
- apache server (192.168.0.1)
- tomcat1 (192.168.0.2)
- tomcat2 (192.168.0.3)

### wokers.properties
```
worker.list=loadbalancer

worker.loadbalancer.type=lb
worker.loadbalancer.balance_workers=was1,was2

worker.was1.type=ajp13
worker.was1.host=localhost
worker.was1.port=8009
worker.was1.lbfactor=1

worker.was2.type=ajp13
worker.was2.host=localhost
worker.was2.port=8099
worker.was2.lbfactor=1
```

## httpd.conf
```bash
LoadModule jk_module modules/mod_jk.so
<IfModule jk_module>
  JkWorkersFile conf/workers.properties 

  JkLogStampFormat "[%a %b %d %H: %M: %S %Y]" 
  JkLogFile "|bin/rotatelogs.exe -l logs/mod_jk_%Y%m%d.log 86400" 
  JkLogLevel Info 

  JkMount /* loadbalancer
</IfModule>
```
