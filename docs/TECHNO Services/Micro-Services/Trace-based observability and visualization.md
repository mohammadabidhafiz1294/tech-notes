While log-based observability is a traditional approach to monitoring and troubleshooting software, as microservices architectures become more complex, log-based observability becomes less efficient. This is because logs don’t collect all needed event-based data. They are typically stored in a centralized location, which can make it difficult to correlate logs from different microservices. Furthermore, they can be voluminous, which makes it difficult to find relevant information, especially when it comes to the flows between microservices. 

Trace-based observability, on the other hand, uses a technique called distributed tracing to track requests as they flow through a microservices architecture. Distributed tracing allows you to see the entire request lifecycle, from the initial request to the final response. This information can be used to identify performance bottlenecks, troubleshoot errors, and improve the overall performance of the application. Distributed tracing is based on code instrumentation is the process of adding code to a microservice to collect telemetry data. code instrumentation can be done manually or automatically.

One of the most popular tools for distributed tracing is [OpenTelemetry’s](https://gethelios.dev/opentelemetry-a-full-guide/) open-source software. It enables the extraction of telemetry data through instrumentation. However, to make OTel effective there’s a need to collect and host the data, analyze it, visualize traces, and provoke alerts as well. [Helios](https://gethelios.dev/) is a tool that’s based on OTel but also includes E2E distributed tracing observability, allowing developers to easily implement OpenTelemety, visualize traces and troubleshoot issues as quickly as possible, lowering MTTR by 90%

Detection (Automatic alerts): 

When running diagnostics, additional data is provided. The screen below shows an example for diagnosis (not related to the alert above, in this case): 

Troubleshooting (root cause analysis) – an example for tace based visualization with granular data (not related to the above): 

Related real-life examples:

[How Novacy Shortened Troubleshooting Time by 90%](https://gethelios.dev/blog/how-novacy-shortened-troubleshooting-time-by-90-with-helios/)

[How Salt Security slashed detection and resolution time in half](https://gethelios.dev/blog/how-we-slashed-detection-and-resolution-time-in-half-salt-security/)