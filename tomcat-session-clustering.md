## 아파치 + 톰캣 구성에서의 세션 클러스터링
![tomcat-session-clustering drawio](https://user-images.githubusercontent.com/13326651/222946654-7da5814e-a421-411f-813e-f0d2899eb162.png)

### ❗️mod.jk 연동이 완료 되었다는 가정하에 진행되었습니다.


### ~application 클래스에 ServletWebServerFactory 설정을 추가한다.
```java
@SpringBootApplication
public class WasApplication {
  public static void main(String[] args) {
    SpringApplication.run(WasApplication.class, args);
  }

  private static boolean distributable;

  public static boolean getDistributable() {
    return distributable;
  }

  @Bean
  public ServletWebServerFactory tomcatFactory() {
    return new TomcatServletWebServerFactory() {
      @Override
      protected void postProcessContext(Context context) {
        WasTestApplication.distributable = context.getDistributable();
      }
    };
  }
}
```

### wokers.properties (Apache)
```
worker.list=loadbalancer

worker.loadbalancer.type=lb
worker.loadbalancer.balance_workers=was1,was2

worker.was1.type=ajp13
worker.was1.host=43.201.1.81
worker.was1.port=8009
worker.was1.lbfactor=1

worker.was2.type=ajp13
worker.was2.host=43.201.1.82
worker.was2.port=8010
worker.was2.lbfactor=1
```

## httpd.conf (Apache)
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

## Server.xml (Tomcat)
### WAS1
```bash
<Connector protocol="AJP/1.3" port="8009" redirectPort="8443" secretRequired="false"/>
```

```bash
<Engine name="Catalina" defaultHost="43.201.1.81" jvmRoute="was1">
  <Cluster className="org.apache.catalina.ha.tcp.SimpleTcpCluster" channelSendOptions="8"> 
      <Manager className="org.apache.catalina.ha.session.DeltaManager" expireSessionsOnShutdown="false" notifyListenersOnReplication="true"/> 
      <Channel className="org.apache.catalina.tribes.group.GroupChannel"> 
          <Membership className="org.apache.catalina.tribes.membership.McastService" 
              address="228.0.0.4" 
              port="45564" 
              frequency="500" 
              dropTime="3000"/>
          <Receiver className="org.apache.catalina.tribes.transport.nio.NioReceiver" 
              address="auto"
              port="4000" 
              autoBind="10" 
              selectorTimeout="5000" 
              maxThreads="6"/> 
          <Sender className="org.apache.catalina.tribes.transport.ReplicationTransmitter"> 
              <Transport className="org.apache.catalina.tribes.transport.nio.PooledParallelSender"/> 
          </Sender> 
          <Interceptor className="org.apache.catalina.tribes.group.interceptors.TcpFailureDetector"/> 
          <Interceptor className="org.apache.catalina.tribes.group.interceptors.MessageDispatchInterceptor"/> 
      </Channel> 
      <Valve className="org.apache.catalina.ha.tcp.ReplicationValve" filter=""/> 
      <Valve className="org.apache.catalina.ha.session.JvmRouteBinderValve"/> 
      <ClusterListener className="org.apache.catalina.ha.session.ClusterSessionListener"/> 
  </Cluster>
  
  <Host>...</Host>
</Engine>
```

### WAS2
```bash
<Connector protocol="AJP/1.3" port="8010" redirectPort="8443" secretRequired="false"/>
```

```bash
<Engine name="Catalina" defaultHost="43.201.1.82" jvmRoute="was2">
  <Cluster className="org.apache.catalina.ha.tcp.SimpleTcpCluster" channelSendOptions="8"> 
      <Manager className="org.apache.catalina.ha.session.DeltaManager" expireSessionsOnShutdown="false" notifyListenersOnReplication="true"/> 
      <Channel className="org.apache.catalina.tribes.group.GroupChannel"> 
          <Membership className="org.apache.catalina.tribes.membership.McastService" 
              address="228.0.0.4" 
              port="45564" 
              frequency="500" 
              dropTime="3000"/>
          <Receiver className="org.apache.catalina.tribes.transport.nio.NioReceiver" 
              address="auto"
              port="4000" 
              autoBind="10" 
              selectorTimeout="5000" 
              maxThreads="6"/> 
          <Sender className="org.apache.catalina.tribes.transport.ReplicationTransmitter"> 
              <Transport className="org.apache.catalina.tribes.transport.nio.PooledParallelSender"/> 
          </Sender> 
          <Interceptor className="org.apache.catalina.tribes.group.interceptors.TcpFailureDetector"/> 
          <Interceptor className="org.apache.catalina.tribes.group.interceptors.MessageDispatchInterceptor"/> 
      </Channel> 
      <Valve className="org.apache.catalina.ha.tcp.ReplicationValve" filter=""/> 
      <Valve className="org.apache.catalina.ha.session.JvmRouteBinderValve"/> 
      <ClusterListener className="org.apache.catalina.ha.session.ClusterSessionListener"/> 
  </Cluster>
  
  <Host>...</Host>
</Engine>
```

