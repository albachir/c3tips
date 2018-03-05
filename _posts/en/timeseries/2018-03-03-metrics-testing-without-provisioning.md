---
layout: post

title: Metrics testing without provisioning
tip-number: 1
tip-username: bachirooov
tip-username-profile: https://www.twitter.com/bachirooov
tip-tldr: Metrics testing without provisioning using `evalMetricsWithMetadata`.

categories:
    - en
    - timeseries
---

# Metrics testing without provisioning

Define a new metric

```javascript
var metric = SimpleMetric.make({
	id:"ActivePowerLouis_WindTurbine", 
	srcType:WindTurbine, 
	name:"ActivePowerLouis", 
	path:"measurements.(name == 'active_power')", 
	expression:"avg(avg(normalized.data.quantity))"})

var spec = EvalMetricsSpec.make({
	start:"2017-01-01", 
	end:"2018-01-01", 
	interval:"DAY", 
	ids:['BEBUB.SS001.WT001'], 
	expressions:['ActivePowerLouis']})
```
Standard evalMetrics will fail because your metric is not available in DB
```javascript
WindTurbine.evalMetrics(spec)

C3.client.ActionError {name: "ActionError", message: "MetricEngine error :  ↵Metric with name 'ActivePow…or type 'WindTurbine' not found! Check seed data!"...}
```

`EvalMetricsWithMetadata` allows you to pass one or multiple metrics on the fly, `evalMetrics` logic will look there first to see if you wrote (or overwrote) a metric, then go to DB if necessary

```javascript
WindTurbine.evalMetricsWithMetadata(spec, [metric])
```

Convert it to JSON before copy pasting into apps
``` javascript
Object.toJSON(metric)
{"type":"SimpleMetric","id":"ActivePowerLouis_WindTurbine","srcType":{"typeName":"WindTurbine"},"name":"ActivePowerLouis","path":"measurements.(name == 'active_power')","expression":"avg(avg(normalized.data.quantity))"}
```
