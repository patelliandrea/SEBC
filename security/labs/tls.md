## Enable TLS Level 1
In order to enable TLS, a keystore has to be created beforehand. To do that, run on the host where cloudera server is running:
```
[ec2-user@ip-172-20-0-4 ~]$ sudo keytool -genkeypair -alias ip-172-20-0-6 -keyalg RSA -keystore \
/opt/cloudera/security/jks/ip-172-20-0-6-keystore.jks -keysize 2048 -dname \
"CN=cmhost.sec.example.com,OU=Security,O=Example,L=Denver,ST=Colorado,C=US" \
-storepass password -keypass password
```

The first step is to enable "Use TLS Encryption for Agents" to true in Administration->Settings->Security.

The next step is to replace `use_tls=0` to `use_tls=1` in `/etc/cloudera-scm-agent/config.init` on every node.

Restart cloudera manager server:
```
[ec2-user@ip-172-20-0-4 ~]$ sudo service cloudera-scm-server restart
```

And restart on every host the cloudera agent:
```
[ec2-user@ip-172-20-0-4 ~]$ ansible padrinocluster -a "sudo service cloudera-scm-agent restart"
```


## Issues encountered
If you don't create the keystore beforehand, once the agents are restarted, cloudera manager is not reachable anymore. Looking at the Cloudera Manager server logs (`/var/log/cloudera-scm-server/cloudera-scm-server.log`) the following error happened:
```
2016-11-16 12:12:18,068 WARN MainThread:org.mortbay.log: failed SslSelectChannelConnector@0.0.0.0:7182: java.io.FileNotFoundException: /var/lib/cloudera-scm-server/.keystore (No such file or directory)
2016-11-16 12:12:18,068 WARN MainThread:org.mortbay.log: failed Server@5d0f32ef: java.io.FileNotFoundException: /var/lib/cloudera-scm-server/.keystore (No such file or directory)
2016-11-16 12:12:18,068 ERROR MainThread:com.cloudera.server.cmf.Main: Failed to start Agent listener.
2016-11-16 12:12:18,069 ERROR MainThread:com.cloudera.server.cmf.Main: Server failed.
org.apache.avro.AvroRuntimeException: java.io.FileNotFoundException: /var/lib/cloudera-scm-server/.keystore (No such file or directory)
        at com.cloudera.server.common.HttpConnectorServer.start(HttpConnectorServer.java:89)
        at com.cloudera.server.cmf.Main.startAgentServer(Main.java:572)
        at com.cloudera.server.cmf.Main.startAvro(Main.java:483)
        at com.cloudera.server.cmf.Main.run(Main.java:620)
        at com.cloudera.server.cmf.Main.main(Main.java:217)
Caused by: java.io.FileNotFoundException: /var/lib/cloudera-scm-server/.keystore (No such file or directory)
        at java.io.FileInputStream.open0(Native Method)
        at java.io.FileInputStream.open(FileInputStream.java:195)
        at java.io.FileInputStream.<init>(FileInputStream.java:138)
        at org.mortbay.resource.FileResource.getInputStream(FileResource.java:275)
        at org.mortbay.jetty.security.SslSelectChannelConnector.createSSLContext(SslSelectChannelConnector.java:639)
        at org.mortbay.jetty.security.SslSelectChannelConnector.doStart(SslSelectChannelConnector.java:613)
        at org.mortbay.component.AbstractLifeCycle.start(AbstractLifeCycle.java:50)
        at org.mortbay.jetty.Server.doStart(Server.java:235)
        at org.mortbay.component.AbstractLifeCycle.start(AbstractLifeCycle.java:50)
        at com.cloudera.server.common.HttpConnectorServer.start(HttpConnectorServer.java:87)
        ... 4 more
2016-11-16 12:12:32,405 INFO ScmActive-0:com.cloudera.server.cmf.components.ScmActive: ScmActive completed successfully.
2016-11-16 12:13:18,473 INFO Thread-11:org.springframework.context.support.ClassPathXmlApplicationContext: Closing ApplicationContext 'rootContext': startup date [Wed Nov 16 12:11:44 EST 2016]; parent: org.springframework.context.support.GenericApplicationContext@1f2586d6
2016-11-16 12:13:18,475 INFO Thread-11:org.springframework.beans.factory.support.DefaultListableBeanFactory: Destroying singletons in org.springframework.beans.factory.support.DefaultListableBeanFactory@335f5c69: defining beans [contextApplicationContextProvider,org.springframework.beans.factory.config.PropertyPlaceholderConfigurer#0,sessionRegistry,passwordEncoder,sslHelper,securityUtils,processStalenessDetector,processStalenessInterceptor,scmParamTrackerStoreImpl,processHelper,releaseDetector,paramResolver,configHelper,dynamicServiceHandlerFactory,configWriterFactory,runnerDescriptorProcessFactory,compatibilityFactory,providesFactory,kerberosPrincProvider,auxConfigGeneratorFactory,configGeneratorFactory,peerConfigGeneratorFactory,zkServerInitListener,solrLoadBalancerConfigUpdateListener,solrAuthenticationConfigUpdateListener,hbaseThriftServerSecurityListener,hbaseRestServerSecurityListener,HBaseZkConfigUpdateListener,HBaseIndexerAuthenticationConfigUpdateListener,dssdToggleListener.PreCommit,dssdToggleListener.PostCommit,oozieLoadBalancerConfigUpdateListener,cmfSchedulerImpl,scheduleManagerImpl,diagnosticsDataUploadHelper,commandStorage,stalenessChecker,commandManager,callableFactory,dirtyParametersListener,metricSchemaGeneration,viewFactory,predefinedPlots,predefinedViews,metricSchemaManagerBean,monitoringTypesInitializer,workAggregatesConfigListener,heartbeatCheckerImpl,logSearchEventsCollectorImpl,serverLogFetcherImpl,ServerLogSearchResponse,agentLogFetcherImpl,descriptorFactory,embeddedDbManager,scmDbValueStore,firehoseRequestService,trialEventAuditor,cmServerState,clouderaManagerMetricsForwarder,currentUserManagerImpl,operationalReportsDisabledListener,licensedFeatureManager,cmUpgradeHelper,operationsManagerImpl,userSettingTransactionManagerImpl,trialEventStalenessCheckTrigger,licenseManagerImpl,navigatorDisabledListener,scmActive,serviceDataProviderBean,authorizer,actionablesProviderImpl,clientProtocolImpl,hostTemplateManagerImpl,sessionServiceImpl,idleSessionManagerImpl,beanConfiguration,cloudStatusDeterminer,jythonObjectFactoryImpl,pythonInterpreterFactory,parcelDependencyManagerImpl,localParcelManagerImpl,parcelInstallerImpl,parcelUpdateService,parcelManagerImpl,agentParcelProviderImpl,parcelStatusProviderImpl,parcelDownloaderImpl,periodicParcelTasks,parcelRepoConfigUpdateListener,parameterFactory,csdTranslationManager,mdlRegistry,csdRegistryImpl,csdManager,csdLocalRepository,validatorConfiguration,prototypeFactory,org.springframework.context.annotation.internalConfigurationAnnotationProcessor,org.springframework.context.annotation.internalAutowiredAnnotationProcessor,org.springframework.context.annotation.internalRequiredAnnotationProcessor,org.springframework.context.annotation.internalCommonAnnotationProcessor,rulesEngine,getObjectMapper,agentAsyncClient,newHeartbeatRequester,commandRequestsBean,getSupportedLocale,newServiceHandlerRegistry,newEventStoreClientFactory,newAutoUpgradeHandlerRegistry,newUpgradeHandlerRegistry,newAgentResultFetcher,newCmfEntityManager,newDatabaseSizeGauge,newCdhExecutorFactory,databaseExecutor,builtInServiceTypes,builtInRoleTypes,builtInNamesForCrossEntityAggregateMetrics,builtInMetricEntityAttributes,builtInMetricEntityTypes,uniqueFieldValidator,requiresSubdirValidator,validServiceDependencyValidator,uniqueServiceTypeValidator,uniqueRoleTypeValidator,existingServiceTypeValidator,existingRoleTypeValidator,expressionValidator,autoConfigSharesValidValidator,messageInterpolator,sdlParser,mdlParser,parcelParser,alternativesParser,permissionsParser,manifestParser,stringInterpolator,serviceDescriptorValidator,serviceMonitoringDefinitionsDescriptorValidator,descriptorVisitor,referenceValidator,parcelDescriptorValidator,alternativesDescriptorValidator,permissionsDescriptorValidator,manifestDescriptorValidator,defaultValidatorConfiguration,springConstraintValidatorFactory,validatorFactoryBean,metricNameFormatValidator,nameForCrossEntityAggregateFormatValidator,objectMapper]; parent: org.springframework.beans.factory.support.DefaultListableBeanFactory@7c9d8e2
2016-11-16 12:13:18,477 INFO Thread-11:com.cloudera.server.cmf.components.ScmActive: ScmActive shutting down.
2016-11-16 12:13:18,477 INFO metric-schema-updater:com.cloudera.cmon.components.MetricSchemaManager: Breaking from sleep in schema update thread.

```

### Restore previous state
To disable TLS, the first step is to stop `cloudera-scm-server` on the server node and `cloudera-scm-agent on every node.

Then we need to replace `use_tls=1` to `use_tls=0` in `/etc/cloudera-scm-agent/config.init` on every node.

Since cloudera manager server stores its configurations on the mysql database, we need to disable "Use TLS Encryption for Agent" from the database:
```
[ec2-user@ip-172-20-0-4 ~]$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 10342
Server version: 5.6.34-log MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> use scm
Database changed
mysql> UPDATE CONFIGS SET value='false' where attr="agent_tls";
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

