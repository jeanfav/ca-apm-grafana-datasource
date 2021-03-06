# CA APM Grafana Data Source

CA APM data source for Grafana, based on the [Metrics Data Web Service (SOAP)](https://docops.ca.com/ca-apm/10-5/en/integrating/api-reference/ca-introscope-web-services-api-reference/polling-web-services/metrics-data-web-service)

This software is not affiliated with or supported by CA Technologies.

## Features
* Visualize CA APM (fka Introscope) metrics in Grafana dashboards (time series format)
* Query Builder: Browse available metrics to construct a metric query
* Refine the query afterwards with basic regular expressions, e.g. wildcards
* Raw Query Mode: Construct your query manually to leverage all regex features
* Use query-based variables for templating (agents and metrics)
* Automatic character escaping, can be disabled

![Demo-Recording](https://github.com/NovaTecConsulting/ca-apm-grafana-datasource/blob/master/media/query-demo.gif)

Just copy the contents of this repository to the plugin directory of your Grafana installation. Assuming the default data path, you should end up with `/var/lib/grafana/plugins/ca-apm-datasource` (Linux) or `<Grafana home>/data/plugins/ca-apm-datasource` (Windows) for example. Only the dist directory is required.

If you use Docker you can just mount the appropriate path. For example:
```
docker run \
  -d \
  --name=grafana \
  -p 3000:3000 \
  -v <absolute path to data source on host>:/var/lib/grafana/plugins/ca-apm-datasource \
  grafana/grafana
```

## Data Source Configuration
To configure a CA APM data source in Grafana, you just have to provide the APM Enterprise Manager's API endpoint and proper authentication details (HTTP basic authentication). The specified user must be authorized to use the Metrics Data Web Service. Click "Save & Test" to make sure that your configuration works correctly.

![Data Source Config](https://github.com/NovaTecConsulting/ca-apm-grafana-datasource/blob/master/media/data-source-config.jpg)

## Metric Queries
To construct a metric query, first create a new panel on a dashboard and select a CA APM data source.
### Query Builder
When you add a new query for a panel, the query builder mode is used by default. Simply click the respective buttons to browse and select agent, metric, and data frequency for your query.
### Raw Query Mode
Click "Toggle Edit Mode" on the right-hand triple bar menu to switch to raw query mode. Although the query builder mode supports basic regular expressions, you can use the raw query mode to use more advanced regex features. Some regular expressions might require that you disable automatic escaping by toggling the respective checkbox.

### Query Variables
You can create variables for templating based on APM queries. You can either query for agents or metrics. For agents, prepend your agent regex with "Agents|", for metrics use "Metrics|" instead. For example, "Agents|.+" will get you all agents. Use the regex option to transform your query results. See the animation below for an example of an agent query:
![Demo-Recording](https://github.com/NovaTecConsulting/ca-apm-grafana-datasource/blob/master/media/query_variables.gif)

### Temporal Resolution Variable
Considering the different temporal aggregation levels of CA APM, it makes sense to use a template variable to control the temporal resolution of time series data dynamically. Simply create a custom dashboard variable and use `15s,30s,1m,2m,6m,12m,24m,48m,1h,168m,12h` for the values.

## License

Copyright (c) 2017 NovaTec Consulting GmbH. All rights reserved.

Licensed under the [MIT](LICENSE.md) License.

## Issues, Feedback and Support
If you experience any issues, have some feedback, or are interested in support, contact us here on GitHub or via email at apm@novatec-gmbh.de.