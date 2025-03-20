---
title: 1.4 Resource Metadata
linkTitle: 1.4 Resource Metadata
weight: 3
hidden: true
---

So far, we've simply exported an exact copy of the span sent through the OpenTelemetry Collector.

Now, let's improve the base span by adding metadata with processors. This extra information can be helpful for troubleshooting and correlation.

{{% notice title="Exercise" style="green" icon="running" %}}
**Stop the collector**: In your **Agent terminal** window, and stop the running collector by pressing `Ctrl-C`. Once the `agent` has stopped, open the `agent.yaml`.

**Update All Pipelines**: Add both processors (`resourcedetection` and `resource/add_mode`) to the `processors` array in **all pipelines**. Ensure `memory_limiter` remains the first processor.

- The [**Resource Detection Processor**](https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/processor/resourcedetectionprocessor/README.md) is used to detect resource information from the host and append or override the resource value in telemetry data with this information.
- The [**Resource Processor**](https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/processor/resourceprocessor/README.md) is used to apply changes on resource attributes. In this case, the default configuration adds a new attribute `otelcol.service.mode` with the value `agent`.

```yaml
service:                          # Services configured for this Collector
  extensions:                     # Enabled extensions
  - health_check
  pipelines:                      # Array of configured pipelines
    traces:
      receivers:
      - otlp                      # OTLP Receiver
      processors:
      - memory_limiter            # Memory Limiter Processor
      - resourcedetection         # Adds system attributes to the data
      - resource/add_mode         # Adds collector mode metadata
      exporters:
      - debug                     # Debug Exporter
      - file                      # File Exporter
    metrics:
      receivers:
      - otlp                      # OTLP Receiver
      processors:
      - memory_limiter            # Memory Limiter Processor
      - resourcedetection         # Adds system attributes to the data
      - resource/add_mode         # Adds collector mode metadata
      exporters:
      - debug                     # Debug Exporter
      - file                      # File Exporter
    logs:
      receivers:
      - otlp                      # OTLP Receiver
      processors:
      - memory_limiter            # Memory Limiter Processor
      - resourcedetection         # Adds system attributes to the data
      - resource/add_mode         # Adds collector mode metadata
      exporters:
      - debug                     # Debug Exporter
      - file                      # File Exporter

```

{{% /notice %}}

By adding these processors, we enrich the data with system metadata and the agent’s operational mode, which aids in troubleshooting and provides useful context for related content.

Validate the agent configuration using **[otelbin.io](https://www.otelbin.io/)**:

```mermaid
%%{init:{"fontFamily":"monospace"}}%%
graph LR
    %% Nodes
      REC1(&nbsp;&nbsp;otlp&nbsp;&nbsp;<br>fa:fa-download):::receiver
      PRO1(memory_limiter<br>fa:fa-microchip):::processor
      PRO2(resourcedetection<br>fa:fa-microchip):::processor
      PRO3(resource<br>fa:fa-microchip<br>add_mode):::processor
      EXP1(&ensp;debug&ensp;<br>fa:fa-upload):::exporter
      EXP2(&ensp;file&ensp;<br>fa:fa-upload):::exporter
    %% Links
    subID1:::sub-traces
    subgraph " "
      subgraph subID1[**Traces/Metrics/Logs**]
      direction LR
      REC1 --> PRO1
      PRO1 --> PRO2
      PRO2 --> PRO3
      PRO3 --> EXP1
      PRO3 --> EXP2
      end
    end
classDef receiver,exporter fill:#8b5cf6,stroke:#333,stroke-width:1px,color:#fff;
classDef processor fill:#6366f1,stroke:#333,stroke-width:1px,color:#fff;
classDef con-receive,con-export fill:#45c175,stroke:#333,stroke-width:1px,color:#fff;
classDef sub-traces stroke:#fff,stroke-width:1px, color:#fff,stroke-dasharray: 3 3;
```
