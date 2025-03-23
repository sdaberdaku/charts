# trino

![Version: 0.15.0](https://img.shields.io/badge/Version-0.15.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 435](https://img.shields.io/badge/AppVersion-435-informational?style=flat-square)

Fast distributed SQL query engine for big data analytics that helps you explore your data universe

**Homepage:** <https://trino.io/>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| Sebastian Daberdaku | <sebastiandaberdaku@gmail.com> |  |

## Source Code

* <https://github.com/trinodb/charts>
* <https://github.com/trinodb/trino/tree/master/core/docker>

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| image.repository | string | `"trinodb/trino"` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.tag | int | `435` |  |
| imagePullSecrets[0].name | string | `"registry-credentials"` |  |
| server.workers | int | `2` |  |
| server.node.environment | string | `"production"` |  |
| server.node.dataDir | string | `"/data/trino"` |  |
| server.node.pluginDir | string | `"/usr/lib/trino/plugin"` |  |
| server.log.trino.level | string | `"INFO"` |  |
| server.config.path | string | `"/etc/trino"` |  |
| server.config.http.port | int | `8080` |  |
| server.config.https.enabled | bool | `false` |  |
| server.config.https.port | int | `8443` |  |
| server.config.https.keystore.path | string | `""` |  |
| server.config.authenticationType | string | `""` |  |
| server.config.query.maxMemory | string | `"43500MB"` |  |
| server.exchangeManager.name | string | `"filesystem"` |  |
| server.exchangeManager.baseDir | string | `"/tmp/trino-local-file-system-exchange-manager"` |  |
| server.workerExtraConfig | string | `""` |  |
| server.coordinatorExtraConfig | string | `""` |  |
| server.autoscaling.enabled | bool | `false` |  |
| server.autoscaling.maxReplicas | int | `5` |  |
| server.autoscaling.targetCPUUtilizationPercentage | int | `50` |  |
| accessControl.type | string | `"configmap"` |  |
| accessControl.refreshPeriod | string | `"60s"` |  |
| accessControl.configFile | string | `"rules.json"` |  |
| accessControl.deltaLakeRules.catalogs[0].user | string | `"admin"` |  |
| accessControl.deltaLakeRules.catalogs[0].catalog | string | `".*"` |  |
| accessControl.deltaLakeRules.catalogs[0].allow | string | `"all"` |  |
| accessControl.deltaLakeRules.catalogs[1].user | string | `"no_admin"` |  |
| accessControl.deltaLakeRules.catalogs[1].catalog | string | `".*"` |  |
| accessControl.deltaLakeRules.catalogs[1].allow | string | `"all"` |  |
| accessControl.deltaLakeRules.schemas[0].user | string | `"admin"` |  |
| accessControl.deltaLakeRules.schemas[0].owner | bool | `true` |  |
| accessControl.deltaLakeRules.schemas[0].schema | string | `".*"` |  |
| accessControl.deltaLakeRules.schemas[1].user | string | `"no_admin"` |  |
| accessControl.deltaLakeRules.schemas[1].owner | bool | `false` |  |
| accessControl.deltaLakeRules.tables | list | `[]` |  |
| accessControl.otherRules.catalogs | list | `[]` |  |
| accessControl.otherRules.schemas | list | `[]` |  |
| accessControl.otherRules.tables | list | `[]` |  |
| additionalNodeProperties | object | `{}` |  |
| additionalConfigProperties | object | `{}` |  |
| additionalLogProperties | object | `{}` |  |
| additionalExchangeManagerProperties | object | `{}` |  |
| eventListenerProperties | object | `{}` |  |
| sharedSecret | string | `""` |  |
| additionalCatalogs | object | `{}` |  |
| deltaLakeCatalogs | object | `{}` |  |
| defaultDeltaLakeCatalogProperties | string | `"hive.metastore=glue\nhive.metastore-cache-ttl=2h\nhive.s3.max-connections=1000\ndelta.metadata.cache-size=2000\ndelta.metadata.cache-ttl=2h\ndelta.metadata.live-files.cache-size=10GB\ndelta.metadata.live-files.cache-ttl=2h\ndelta.enable-non-concurrent-writes=true\ndelta.unique-table-location=false\ndelta.compression-codec=SNAPPY\ndelta.table-statistics-enabled=true\ndelta.extended-statistics.enabled=true\n"` |  |
| env | list | `[]` |  |
| envFrom | list | `[]` |  |
| initContainers | object | `{}` |  |
| sidecarContainers | object | `{}` |  |
| securityContext.runAsUser | int | `1000` |  |
| securityContext.runAsGroup | int | `1000` |  |
| securityContext.fsGroup | int | `1000` |  |
| securityContext.fsGroupChangePolicy | string | `"OnRootMismatch"` |  |
| shareProcessNamespace.coordinator | bool | `false` |  |
| shareProcessNamespace.worker | bool | `false` |  |
| service.type | string | `"ClusterIP"` |  |
| service.port | int | `8080` |  |
| auth | object | `{}` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `""` |  |
| serviceAccount.annotations | object | `{}` |  |
| secretMounts | list | `[]` |  |
| coordinator.jvm.maxHeapSize | string | `"40500m"` |  |
| coordinator.jvm.gcMethod.type | string | `"UseG1GC"` |  |
| coordinator.jvm.gcMethod.g1.heapRegionSize | string | `"32M"` |  |
| coordinator.config.memory.heapHeadroomPerNode | string | `"12150MB"` |  |
| coordinator.config.query.maxMemoryPerNode | string | `"12150MB"` |  |
| coordinator.additionalJVMConfig | object | `{}` |  |
| coordinator.additionalExposedPorts | object | `{}` |  |
| coordinator.resources.requests.cpu | string | `"15000m"` |  |
| coordinator.resources.requests.memory | string | `"55000Mi"` |  |
| coordinator.resources.limits.memory | string | `"55000Mi"` |  |
| coordinator.livenessProbe | object | `{}` |  |
| coordinator.readinessProbe | object | `{}` |  |
| coordinator.nodeSelector.dedicated | string | `"trino"` |  |
| coordinator.tolerations[0].key | string | `"dedicated"` |  |
| coordinator.tolerations[0].value | string | `"trino"` |  |
| coordinator.affinity | object | `{}` |  |
| coordinator.additionalConfigFiles | object | `{}` |  |
| coordinator.annotations | object | `{}` |  |
| coordinator.labels | object | `{}` |  |
| coordinator.secretMounts | list | `[]` |  |
| coordinator.metrics | object | `{}` |  |
| worker.jvm.maxHeapSize | string | `"40500m"` |  |
| worker.jvm.gcMethod.type | string | `"UseG1GC"` |  |
| worker.jvm.gcMethod.g1.heapRegionSize | string | `"32M"` |  |
| worker.config.memory.heapHeadroomPerNode | string | `"12150MB"` |  |
| worker.config.query.maxMemoryPerNode | string | `"12150MB"` |  |
| worker.additionalJVMConfig | object | `{}` |  |
| worker.additionalExposedPorts | object | `{}` |  |
| worker.resources.requests.cpu | string | `"15000m"` |  |
| worker.resources.requests.memory | string | `"55000Mi"` |  |
| worker.resources.limits.memory | string | `"55000Mi"` |  |
| worker.livenessProbe | object | `{}` |  |
| worker.readinessProbe | object | `{}` |  |
| worker.nodeSelector.dedicated | string | `"trino"` |  |
| worker.tolerations[0].key | string | `"dedicated"` |  |
| worker.tolerations[0].value | string | `"trino"` |  |
| worker.affinity | object | `{}` |  |
| worker.additionalConfigFiles | object | `{}` |  |
| worker.annotations | object | `{}` |  |
| worker.labels | object | `{}` |  |
| worker.secretMounts | list | `[]` |  |
| worker.metrics | object | `{}` |  |
| kafka.mountPath | string | `"/etc/trino/schemas"` |  |
| kafka.tableDescriptions | object | `{}` |  |
| commonLabels | object | `{}` |  |
| ingress.extraAnnotations | object | `{}` |  |
| ingress.certificateArn | string | `""` |  |
| ingress.hostname | string | `""` |  |
| networkPolicy | object | `{}` |  |
| logsVolume.storageClassName | string | `"efs"` |  |
| logsVolume.storageSize | string | `"10Gi"` |  |
| resourceGroups.rootGroups[0].name | string | `"equalizer"` |  |
| resourceGroups.rootGroups[0].maxQueued | int | `1000` |  |
| resourceGroups.rootGroups[0].hardConcurrencyLimit | int | `1000` |  |
| resourceGroups.rootGroups[0].softMemoryLimit | string | `"100%"` |  |
| resourceGroups.rootGroups[0].jmxExport | bool | `true` |  |
| resourceGroups.rootGroups[1].name | string | `"not_equalizer"` |  |
| resourceGroups.rootGroups[1].maxQueued | int | `100` |  |
| resourceGroups.rootGroups[1].hardConcurrencyLimit | int | `30` |  |
| resourceGroups.rootGroups[1].softMemoryLimit | string | `"40%"` |  |
| resourceGroups.rootGroups[1].jmxExport | bool | `true` |  |
| resourceGroups.selectors[0].user | string | `"equalizer"` |  |
| resourceGroups.selectors[0].group | string | `"equalizer"` |  |
| resourceGroups.selectors[1].user | string | `".*"` |  |
| resourceGroups.selectors[1].group | string | `"not_equalizer"` |  |
| sessionPropertyConfig[0].group | string | `"not-equalizer"` |  |
| sessionPropertyConfig[0].sessionProperties.query_max_execution_time | string | `"5m"` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
