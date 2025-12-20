# spark-connect

![Version: 2.0.0](https://img.shields.io/badge/Version-2.0.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 4.1.0](https://img.shields.io/badge/AppVersion-4.1.0-informational?style=flat-square)

A Helm chart for deploying a Spark-Connect Server on Kubernetes

## Values
* `image.repository` - string, default: `"ghcr.io/sdaberdaku/spark-with-glue"`
* `image.pullPolicy` - string, default: `"IfNotPresent"`
* `image.tag` - string, default: `"4.1.0-scala2.13-java21-python3-ubuntu"`
* `imagePullSecrets` - list, default: `[]`
* `nameOverride` - string, default: `""`
* `fullnameOverride` - string, default: `""`
* `spark.homeDir` - string, default: `"/opt/spark"`  

  Sets the Spark Home directory
* `spark.log4j2` - object, default: `{"enabled":false,"properties":""}`  

  Configure Spark Logging
* `spark.log4j2.enabled` - bool, default: `false`  

  Set to true to apply a custom `log4j2.properties` to configure [logging](https://spark.apache.org/docs/latest/configuration.html#configuring-logging).
* `spark.log4j2.properties` - string, default: `""`  

  Log4j2 (templated) properties to apply.
  Example
  ```yaml
  properties: |-
    rootLogger.level = warn
    rootLogger.appenderRef.stdout.ref = console
  ```
* `spark.metrics` - object, default: `{"enabled":false,"prometheusServletPath":"/metrics","properties":""}`  

  Configure Spark Metrics
* `spark.metrics.enabled` - bool, default: `false`  

  Set to true to apply a custom `metrics.properties` to configure [metrics](https://spark.apache.org/docs/latest/monitoring.html#metrics).
* `spark.metrics.prometheusServletPath` - string, default: `"/metrics"`  

  Path on which the Prometheus metrics are exposed
* `spark.metrics.properties` - string, default: `""`  

  Metrics (templated) properties to apply.
  Example
  ```yaml
  properties: |-
    *.sink.prometheusServlet.class=org.apache.spark.metrics.sink.PrometheusServlet
    *.sink.prometheusServlet.path={{- .Values.spark.metrics.prometheusServletPath }}
  ```
* `spark.scratchDirs` - list, default: `["/tmp"]`  

  A list of directories to use for "scratch" space in Spark, including map output files and RDDs that get stored on disk. These should be on a fast, local disk in your system.
* `spark.packages` - list, default: `[]`  

  A list of Maven coordinates of jars to include on the driver and executor classpaths.
* `spark.kubernetesEndpoint` - string, default: `"https://kubernetes.default.svc.cluster.local:443"`
* `spark.extraProperties` - string, default: `nil`  

  Extra Spark properties to apply to the current deployment. If a property is provided more than once, the last instance will override the previous ones. The value is templated with `tpl`.
  Example
  ```yaml
  extraProperties: |-
    spark.sql.catalogImplementation hive
    spark.dynamicAllocation.enabled true
    spark.dynamicAllocation.executorIdleTimeout 300s
    spark.dynamicAllocation.cachedExecutorIdleTimeout 300s
    spark.dynamicAllocation.initialExecutors 0
    spark.dynamicAllocation.minExecutors 0
    spark.dynamicAllocation.maxExecutors 5
    spark.dynamicAllocation.shuffleTracking.enabled true
    spark.dynamicAllocation.shuffleTracking.timeout 600s
    spark.hadoop.aws.region us-east-2
    spark.hadoop.fs.s3.impl org.apache.hadoop.fs.s3a.S3AFileSystem
    spark.hadoop.fs.s3a.impl org.apache.hadoop.fs.s3a.S3AFileSystem
    spark.hadoop.fs.s3a.aws.credentials.provider software.amazon.awssdk.auth.credentials.WebIdentityTokenFileCredentialsProvider
    spark.hadoop.fs.s3a.endpoint s3.us-east-2.amazonaws.com
    spark.hive.imetastoreclient.factory.class com.amazonaws.glue.catalog.metastore.AWSGlueDataCatalogHiveClientFactory
    spark.hive.aws.catalog.credentials.provider.factory.class software.amazon.awssdk.auth.credentials.WebIdentityTokenFileCredentialsProvider
    spark.hive.aws.glue.endpoint glue.us-east-2.amazonaws.com
    spark.hive.aws.region us-east-2
  ```
* `spark.driver` - object, default: `{"affinity":{"podAntiAffinity":{"preferredDuringSchedulingIgnoredDuringExecution":[{"podAffinityTerm":{"labelSelector":{"matchLabels":{"app.kubernetes.io/component":"spark-driver"}},"topologyKey":"topology.kubernetes.io/zone"},"weight":100},{"podAffinityTerm":{"labelSelector":{"matchLabels":{"app.kubernetes.io/component":"spark-driver"}},"topologyKey":"kubernetes.io/hostname"},"weight":50}]}},"cores":1,"extraEnv":[],"memoryMiB":3072,"memoryOverheadMiB":256,"nodeSelector":{},"podAnnotations":{},"podLabels":{},"requestCoresMilliCPU":1000,"tolerations":[]}`  

  Spark Driver configuration
* `spark.driver.cores` - int, default: `1`  

  Sets the `spark.driver.cores` property. Controls the parallelism of the driver process.
* `spark.driver.requestCoresMilliCPU` - int, default: `1000`  

  Sets the Driver's Pod Cpu request
* `spark.driver.memoryMiB` - int, default: `3072`  

  Spark Driver memory
* `spark.driver.memoryOverheadMiB` - int, default: `256`  

  Spark Driver memory overhead. The Pod Memory request is going to be the sum of `memoryMiB` and `memoryOverheadMiB`
* `spark.driver.podAnnotations` - object, default: `{}`  

  Annotations for the Driver Pod
* `spark.driver.podLabels` - object, default: `{}`  

  Labels for the Driver Pod
* `spark.driver.extraEnv` - list, default: `[]`  

  Environment variables to add to the Driver Pod.
* `spark.driver.nodeSelector` - object, default: `{}`  

  Set the node selector for the Driver Pod.
  Example
  ```yaml
  nodeSelector:
    dedicated: spark-connect-driver
  ```
* `spark.driver.tolerations` - list, default: `[]`  

  Set the tolerations for the Driver Pod.
  Example
  ```yaml
  tolerations:
    - key: dedicated
      value: spark-connect-driver
  ```
* `spark.driver.affinity` - object, default: `{"podAntiAffinity":{"preferredDuringSchedulingIgnoredDuringExecution":[{"podAffinityTerm":{"labelSelector":{"matchLabels":{"app.kubernetes.io/component":"spark-driver"}},"topologyKey":"topology.kubernetes.io/zone"},"weight":100},{"podAffinityTerm":{"labelSelector":{"matchLabels":{"app.kubernetes.io/component":"spark-driver"}},"topologyKey":"kubernetes.io/hostname"},"weight":50}]}}`  

  Set the affinity for the Driver Pod.
* `spark.executor.cores` - int, default: `4`  

  Sets the `spark.executor.cores` property. Controls the parallelism of the executor processes.
* `spark.executor.requestCoresMilliCPU` - int, default: `1000`  

  Sets the Executor Pods Cpu request
* `spark.executor.memoryMiB` - int, default: `3072`  

  Spark Driver memory
* `spark.executor.memoryOverheadMiB` - int, default: `256`  

  Spark Executor memory overhead. The Pod Memory request is going to be the sum of `memoryMiB` and `memoryOverheadMiB`
* `spark.executor.instances` - int, default: `2`  

  The number of executors to run.
* `spark.executor.podAnnotations` - object, default: `{}`  

  Annotations for the Executor Pods
  Example
  ```yaml
  podAnnotations:
    argocd.argoproj.io/compare-options: IgnoreExtraneous
  ```
* `spark.executor.podLabels` - object, default: `{}`  

  Labels for the Executor Pods
* `spark.executor.extraEnv` - list, default: `[]`  

  Environment variables to add to the Executor Pods.
* `spark.executor.nodeSelector` - object, default: `{}`  

  Set the node selector for the Executor Pods.
  Example
  ```yaml
  nodeSelector:
    dedicated: spark-connect-executor
  ```
* `spark.executor.tolerations` - list, default: `[]`  

  Set the tolerations for the Executor Pods.
  Example
  ```yaml
  tolerations:
    - key: dedicated
      value: spark-connect-executor
  ```
* `spark.executor.affinity` - object, default: `{"podAffinity":{"preferredDuringSchedulingIgnoredDuringExecution":[{"podAffinityTerm":{"labelSelector":{"matchLabels":{"app.kubernetes.io/component":"spark-driver"}},"topologyKey":"kubernetes.io/hostname"},"weight":100},{"podAffinityTerm":{"labelSelector":{"matchLabels":{"app.kubernetes.io/component":"spark-executor"}},"topologyKey":"kubernetes.io/hostname"},"weight":75},{"podAffinityTerm":{"labelSelector":{"matchLabels":{"app.kubernetes.io/component":"spark-driver"}},"topologyKey":"topology.kubernetes.io/zone"},"weight":50}],"requiredDuringSchedulingIgnoredDuringExecution":[{"labelSelector":{"matchLabels":{"app.kubernetes.io/component":"spark-executor"}},"topologyKey":"topology.kubernetes.io/zone"}]}}`  

  Set the affinity for the Executor Pods.
* `spark.historyServer.enabled` - bool, default: `false`  

  Set to true to deploy the Spark History Server alongside Spark Connect
* `spark.historyServer.replicas` - int, default: `1`  

  Number of replicas for the Spark History Server Deployment
* `spark.historyServer.extraProperties` - string, default: `nil`  

  Extra Spark properties to apply to the current deployment. If a property is provided more than once, the last instance will override the previous ones. The value is templated with `tpl`.
  Example
  ```yaml
  extraProperties: |-
    spark.spark.plugins: io.dataflint.spark.SparkDataflintPlugin
    spark.dataflint.iceberg.autoCatalogDiscovery: true
* `spark.historyServer.sparkDaemonMemory` - string, default: `"1024m"`  

  Memory allocated to the Spark History Server daemon
* `spark.historyServer.resources` - object, default: `{}`  

  Resource requests and limits for the Spark History Server Pod
  Example
  ```yaml
  resources:
    requests:
      memory: "1Gi"
      cpu: "500m"
    limits:
      memory: "2Gi"
      cpu: "1"
  ```
* `spark.historyServer.podAnnotations` - object, default: `{}`  

  Annotations for the Spark History Server Pods
  Example
  ```yaml
  podAnnotations:
    argocd.argoproj.io/compare-options: IgnoreExtraneous
  ```
* `spark.historyServer.podLabels` - object, default: `{}`  

  Labels for the Spark History Server Pods
* `spark.historyServer.extraEnv` - list, default: `[]`  

  Environment variables to add to the Spark History Server Pods.
* `spark.historyServer.nodeSelector` - object, default: `{}`  

  Set the node selector for the Spark History Server Pods.
  Example
  ```yaml
  nodeSelector:
    dedicated: spark-history-server
  ```
* `spark.historyServer.tolerations` - list, default: `[]`  

  Set the tolerations for the Spark History Server Pods.
  Example
  ```yaml
  tolerations:
    - key: dedicated
      value: spark-history-server
  ```
* `spark.historyServer.affinity` - object, default: `{"podAntiAffinity":{"preferredDuringSchedulingIgnoredDuringExecution":[{"podAffinityTerm":{"labelSelector":{"matchLabels":{"app.kubernetes.io/component":"spark-history-server"}},"topologyKey":"topology.kubernetes.io/zone"},"weight":100}],"requiredDuringSchedulingIgnoredDuringExecution":[{"labelSelector":{"matchLabels":{"app.kubernetes.io/component":"spark-history-server"}},"topologyKey":"kubernetes.io/hostname"}]}}`  

  Set the affinity for the Spark History Server Pods.
* `serviceAccount.create` - bool, default: `true`
* `serviceAccount.automount` - bool, default: `true`
* `serviceAccount.annotations` - object, default: `{}`
* `serviceAccount.name` - string, default: `""`
* `commonPodAnnotations` - object, default: `{}`
* `commonPodLabels` - object, default: `{}`
* `podSecurityContext` - object, default: `{}`
* `securityContext` - object, default: `{}`
* `service.annotations` - object, default: `{}`
* `service.ports.sparkConnect` - int, default: `15002`
* `service.ports.sparkDriver` - int, default: `55000`
* `service.ports.sparkUI` - int, default: `4040`
* `service.ports.sparkHistoryServer` - int, default: `18080`
* `serviceMonitor.enabled` - bool, default: `false`  

  Set to true to create resources for the [prometheus-operator](https://github.com/prometheus-operator/prometheus-operator).
* `serviceMonitor.labels` - object, default: `{}`  

  Labels for serviceMonitor, so that Prometheus can select it
* `serviceMonitor.interval` - string, default: `"30s"`  

  The serviceMonitor web endpoint interval
* `serviceMonitor.metricRelabelings` - list, default: `[]`  

  configures the relabeling rules to apply to the samples before ingestion.
  Example
  ```yaml
  metricRelabelings:
    - sourceLabels: [ __name__ ]
      regex: 'metrics_spark_.*_spark_streaming_(.*)_(eventTime_watermark|inputRate_total|latency|processingRate_total|states_rowsTotal|states_usedBytes)_.*'
      targetLabel: kafkaTopic
      replacement: ${1}
    - sourceLabels: [ __name__ ]
      targetLabel: __name__
      regex: 'metrics_spark_.*_spark_streaming_.*_(eventTime_watermark|inputRate_total|latency|processingRate_total|states_rowsTotal|states_usedBytes)_(Number|Value)'
      replacement: 'spark_streaming_${1}_${2}'
    - sourceLabels: [ __name__ ]
      regex: '^metrics_spark_.*$'
      action: drop
  ```
* `serviceMonitor.relabelings` - list, default: `[]`  

  configures the relabeling rules to apply the target’s metadata labels.
  Example
  ```yaml
  relabelings:
    - sourceLabels: [ __meta_kubernetes_namespace ]
      regex: (.*)
      targetLabel: namespace
      replacement: ${1}
  ```
* `prometheusRule` - object, default: `{"enabled":false,"groups":[],"labels":{}}`  

  The PrometheusRule custom resource definition (CRD) defines alerting and recording rules to be evaluated by Prometheus or ThanosRuler objects.
* `prometheusRule.enabled` - bool, default: `false`  

  Set to true to create resources for the [prometheus-operator](https://github.com/prometheus-operator/prometheus-operator).
* `prometheusRule.labels` - object, default: `{}`  

  Labels for prometheusRule, so that Prometheus can select it
* `prometheusRule.groups` - list, default: `[]`  

  Specification of desired alerting rule definitions for Prometheus.
  Example
  ```yaml
  groups:
    - name: spark-connect
      rules:
        - alert: SparkStreamingQueries
          expr: count(spark_streaming_eventTime_watermark_Number) < 1 or absent(spark_streaming_eventTime_watermark_Number)
          for: 1m
          labels:
            severity: major
          annotations:
            summary: "Spark Streaming Queries down"
            description: "One or more Spark Streaming Queries are not currently running!"
  ```
* `ingress.connect.enabled` - bool, default: `false`
* `ingress.connect.className` - string, default: `""`
* `ingress.connect.annotations` - object, default: `{}`
* `ingress.connect.hosts[0].host` - string, default: `"chart-example.local"`
* `ingress.connect.hosts[0].paths[0].path` - string, default: `"/"`
* `ingress.connect.hosts[0].paths[0].pathType` - string, default: `"ImplementationSpecific"`
* `ingress.connect.tls` - list, default: `[]`
* `ingress.ui.enabled` - bool, default: `false`
* `ingress.ui.className` - string, default: `""`
* `ingress.ui.annotations` - object, default: `{}`
* `ingress.ui.hosts[0].host` - string, default: `"chart-example.local"`
* `ingress.ui.hosts[0].paths[0].path` - string, default: `"/"`
* `ingress.ui.hosts[0].paths[0].pathType` - string, default: `"ImplementationSpecific"`
* `ingress.ui.tls` - list, default: `[]`
* `ingress.historyServer.enabled` - bool, default: `false`
* `ingress.historyServer.className` - string, default: `""`
* `ingress.historyServer.annotations` - object, default: `{}`
* `ingress.historyServer.hosts[0].host` - string, default: `"chart-example.local"`
* `ingress.historyServer.hosts[0].paths[0].path` - string, default: `"/"`
* `ingress.historyServer.hosts[0].paths[0].pathType` - string, default: `"ImplementationSpecific"`
* `ingress.historyServer.tls` - list, default: `[]`

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
