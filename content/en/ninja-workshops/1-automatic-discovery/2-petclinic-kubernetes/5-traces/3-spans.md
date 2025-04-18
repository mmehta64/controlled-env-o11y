---
title: APM Span
linkTitle: 3. APM Spans
weight: 3
---

While we examine our spans, let's look at several out-of-the-box features that you get **without code modifications** when using **automatic discovery and configuration** on top of tracing:

First, in the Waterfall Pane, make sure the `customers-service:SELECT petclinic` or similar span is selected as shown in the screenshot below:

![DB-query](../../images/db-query.png)

* The basic latency information is shown as a bar for the instrumented function or call. In our example above, it took 17.8 Milliseconds.
* Several similar Spans **(1)** are only visible if the span is repeated multiple times. In this case, there are 10 repeats in our example. You can show/hide them all by clicking on the `10x` and all spans will show in order.
* **Inferred Services**: Calls made to external systems that are not instrumented show up as a grey 'inferred' span. The Inferred Service or span in our example is a call to the Mysql Database `mysql:petclinic SELECT petclinic` **(2)** as shown above.
* **Span Tags**: In the Tag Pane, we see standard tags produced by the automatic discovery and configuration. In this case, the span is calling a Database, so it includes the `db.statement` tag **(3)**. This tag will hold the DB query statement and is used by the Database call performed during this span. This will be used by the DB-Query Performance feature. We look at DB-Query Performance in the next section.
* **Always-on Profiling**: **IF** the system is configured to capture Profiling data during a Span life cycle. It will show the number of Call Stacks captured in the Spans timeline. In our example above, we see 18 Call Stacks for the `customer-service:GET /owners` Span. **(4)**

We will look at Profiling in the next section.

<!--
## 3. Review Profiling Data Collection

You can now visit the Splunk APM UI and examine the application components, traces, profiling, DB Query performance and metrics. From the left-hand menu **APM** → **Explore**, click the environment dropdown and select your environment e.g. `<INSTANCE>-petclinic` (where`<INSTANCE>` is replaced with the value you noted down earlier).

![APM Environment](../images/apm-environment.png)

Once your validation is complete you can stop the application by pressing `Ctrl-c`.

## 4. Adding Resource Attributes to Spans

Resource attributes can be added to every reported span. For example `version=0.314`. A comma-separated list of resource attributes can also be defined e.g. `key1=val1,key2=val2`.

Let's launch the PetClinic again using new resource attributes. Note, that adding resource attributes to the run command will override what was defined when we installed the collector. Let's add two new resource attributes `deployment.environment=$INSTANCE-petclinic-env,version=0.314`:

```bash
java \
-Dserver.port=8083 \
-Dotel.service.name=$INSTANCE-petclinic-service \
-Dotel.resource.attributes=deployment.environment=$INSTANCE-petclinic-env,version=0.314 \
-jar target/spring-petclinic-*.jar --spring.profiles.active=mysql
```

Back in the Splunk APM UI we can drill down on a recent trace and see the new `version` attribute in a span.

-->