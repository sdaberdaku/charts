# charts
My custom Helm Chart repository, served from the `gh-pages` branch at https://sdaberdaku.github.io/charts.

## Charts

| Chart | Folder | Latest version | Description |
| --- | --- | --- | --- |
| `spark-connect` | [spark-connect](spark-connect) | 2.0.0 | Spark Connect server on Kubernetes. The default image is `ghcr.io/sdaberdaku/spark-with-glue`. |
| `spark-history-server` | [spark-history-server](spark-history-server) | 1.0.0 | Spark History Server web UI for completed and running Spark applications. |
| `trino` | [trino](trino) | 0.15.0 | Trino 435, based on the official Trino chart from [trinodb/charts](https://github.com/trinodb/charts). |
| `jdbc-connections` | [trino-jdbc-connections](trino-jdbc-connections) | 1.0.0 | JDBC connections stored as Kubernetes secrets, for use by Trino. |
| `karpenter-extra` | [karpenter-extra](karpenter-extra) | 1.0.0 | Karpenter NodeClasses and NodePools. |
| `kyverno-policy` | [kyverno-policy](kyverno-policy) | 1.0.0 | Kyverno ClusterPolicy that forces a nodeSelector and tolerations on all pods of a namespace. |
| `storage-class-with-tags` | [storage-class-with-tags](storage-class-with-tags) | 1.0.0 | Storage class that enforces EBS volume tagging. |
| `secrets` | [airflow-secrets](airflow-secrets) | 1.0.0 | Kubernetes secrets required by Airflow. |
| `spark-addon` | [airflow-spark-addon](airflow-spark-addon) | 1.0.0 | Spark add-ons for Airflow. |

Each folder has a README with the chart's values.

## Using the repository

The current repository can be added with the following command:
```shell
helm repo add sdaberdaku https://sdaberdaku.github.io/charts
```
The repository can then be updated with the following command:
```shell
helm repo update sdaberdaku
```

To view the available charts in the repository you can use:
```shell
helm search repo sdaberdaku
```

To install a chart, for example Spark Connect:
```shell
helm install spark-connect sdaberdaku/spark-connect --namespace spark --create-namespace
```

## Publishing a chart

To build a Helm package use the following command:
```shell
helm package <package-path>
```

After the package has been built, rebuild the index with:
```shell
helm repo index .
```

The chart READMEs are generated with [helm-docs](https://github.com/norwoodj/helm-docs) through the pre-commit hooks in
`.pre-commit-config.yaml`.

## License
[Apache License 2.0](LICENSE)
