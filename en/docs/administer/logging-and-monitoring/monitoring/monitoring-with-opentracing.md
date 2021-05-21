# Enabling Tracing with OpenTracing

In a distributed API Manager architecture, tracing a message is important to debug and observe a message path. This is known as distributed tracing. OpenTracing allows you to enable distributed tracing for WSO2 API Manager.
OpenTracing aims to be an open, vendor-neutral standard for distributed systems instrumentation. It offers a way for developers to follow the thread — to trace requests from beginning to end across touchpoints and understand distributed systems at scale. Open tracing will also help to trace the message and identify the latencies that took place in each process or method. Thereby, open tracing will help you to carry out a time-related analysis.

 WSO2 API Manager supports the following types of ways to retrieve instrumented data.

 - Jaeger
 - Zipkin
 - Log

For more information, see [Open Tracer Configurations]({{base_path}}/reference/config-catalog/#api-m-open-tracer-configurations).

## Enabling Jaeger Tracing

1. Copy the following configuration into the `deployment.toml` file.

    ```toml tab="Format"
    [apim.open_tracer]
    remote_tracer.enable = true
    remote_tracer.name = "jaeger"
    remote_tracer.properties.hostname = "<hostname-of-jaeger-endpoint>"
    remote_tracer.properties.port = "<port-of-jaeger-endpoint>"
    ```

    ```toml tab="Example"
    [apim.open_tracer]
    remote_tracer.enable = true
    remote_tracer.name = "jaeger"
    remote_tracer.properties.hostname = "localhost"
    remote_tracer.properties.port = "6831" 
    #6832 can also be used as the port
    ```

2. Start the server.

     After you invoke the APIs you will see the tracing data in Jaeger as follow:

    [![Distributed tracing jaeger]({{base_path}}/assets/img/administer/opentracing-jaeger.png)]({{base_path}}/assets/img/administer/opentracing-jaeger.png)

## Enabling Zipkin Tracing

1. Copy the following configuration into the `deployment.toml` file.

    ```toml tab="Format"
    [apim.open_tracer]
    remote_tracer.enable = true
    remote_tracer.name = "zipkin"
    remote_tracer.properties.hostname = "<hostname-of-zikin-endpoint>"
    remote_tracer.properties.port = "<port-o-zipkin-endpoint>"
    ```

    ```toml tab="Example"
    [apim.open_tracer]
    remote_tracer.enable = true
    remote_tracer.name = "zipkin"
    remote_tracer.properties.hostname = "localhost"
    remote_tracer.properties.port = "9411"
    ```

2. Start the server.

     After you invoke the APIs you will see the tracing data in Zipkin as follow:

[![Distributed tracing zipkin]({{base_path}}/assets/img/administer/opentracing-zipkin.png)]({{base_path}}/assets/img/administer/opentracing-zipkin.png)


## Enabling Log Tracing
1. Copy the following configuration into the `deployment.toml` file.

    ```toml
    [apim.open_tracer]
    remote_tracer.enable = false
    log_tracer.enable = true
    ```

2. Start the server.

    After you invoke the APIs you will be able to see tracing data in the `wso2-apimgt-open-tracing.log` in the `<API-M_HOME>/repository/logs` folder.

    ```log
    20:19:46,937 [-] [PassThroughMessageProcessor-14] TRACE {"Latency":0,"Operation":"API:CORS_Request_Handler","Tags":{}}
    n20:19:46,938 [-] [PassThroughMessageProcessor-14] TRACE {"Latency":0,"Operation":"API:Get_Client_Domain()","Tags":{}}
    n20:19:46,939 [-] [PassThroughMessageProcessor-14] TRACE {"Latency":0,"Operation":"API:Find_matching_verb()","Tags":{}}
    n20:19:46,939 [-] [PassThroughMessageProcessor-14] TRACE {"Latency":1,"Operation":"API:Get_Resource_Authentication_Scheme()","Tags":{}}
    n20:19:46,956 [-] [https-jsse-nio-9443-exec-23] TRACE {"Latency":0,"Operation":"API:Get_Access_Token_Cache_key()","Tags":{}}
    n20:19:46,958 [-] [https-jsse-nio-9443-exec-23] TRACE {"Latency":0,"Operation":"API:Fetching_API_iNFO_DTO_FROM_CACHE()","Tags":{}}
    n20:19:46,959 [-] [https-jsse-nio-9443-exec-23] TRACE {"Latency":0,"Operation":"API:Validate_Token()","Tags":{}}
    n20:19:46,972 [-] [https-jsse-nio-9443-exec-23] TRACE {"Latency":12,"Operation":"API:Validate_Subscription()","Tags":{}}
    n20:19:46,973 [-] [https-jsse-nio-9443-exec-23] TRACE {"Latency":0,"Operation":"API:Validate_Scopes()","Tags":{}}
    n20:19:46,974 [-] [https-jsse-nio-9443-exec-23] TRACE {"Latency":0,"Operation":"API:Write_To_Key_Manager_Cache()","Tags":{}}
    n20:19:46,975 [-] [https-jsse-nio-9443-exec-23] TRACE {"Latency":0,"Operation":"API:Publishing_Key_Validation_Response","Tags":{}}
    n20:19:46,976 [-] [https-jsse-nio-9443-exec-23] TRACE {"Latency":20,"Operation":"API:Validate_Main","Tags":{}}
    n20:19:46,991 [-] [PassThroughMessageProcessor-14] TRACE {"Latency":51,"Operation":"API:Key_Validation_From_Gateway_Node","Tags":{}}
    n20:19:46,992 [-] [PassThroughMessageProcessor-14] TRACE {"Latency":52,"Operation":"API:Get_Key_Validation_Info()","Tags":{}}
    n20:19:46,993 [-] [PassThroughMessageProcessor-14] TRACE {"Latency":56,"Operation":"API:Key_Validation_Latency","Tags":{}}
    n20:19:46,994 [-] [PassThroughMessageProcessor-14] TRACE {"Latency":0,"Operation":"API:Throttle_Latency","Tags":{}}
    n20:19:46,995 [-] [PassThroughMessageProcessor-14] TRACE {"Latency":0,"Operation":"API:API_Mgt_Usage_Handler","Tags":{}}
    n20:19:46,996 [-] [PassThroughMessageProcessor-14] TRACE {"Latency":1,"Operation":"API:Google_Analytics_Handler","Tags":{}}
    n20:19:46,996 [-] [PassThroughMessageProcessor-14] TRACE {"Latency":0,"Operation":"API:Request_Mediation_Latency","Tags":{}}
    n20:19:47,016 [-] [PassThroughMessageProcessor-15] TRACE {"Latency":19,"Operation":"API:Backend_Latency","Tags":{"span.endpoint":"https://localhost:9443/am/sample/pizzashack/v1/api/"}}
    n20:19:47,017 [-] [PassThroughMessageProcessor-15] TRACE {"Latency":0,"Operation":"API:Response_Mediation_Latency","Tags":{}}
    n20:19:47,018 [-] [PassThroughMessageProcessor-15] TRACE {"Latency":0,"Operation":"API:API_MGT_Response_Handler","Tags":{}}
    n20:19:47,019 [-] [PassThroughMessageProcessor-15] TRACE {"Latency":83,"Operation":"API:Response_Latency","Tags":{"span.resource":"/menu","span.kind":"server","span.api.name":"PizzaShackAPI","span.consumerkey":"Fn9RGuFeefEe7W07jOq_mvQvLJwa","span.request.method":"GET","span.request.path":"pizzashack/1.0.0/menu","span.api.version":"1.0.0","span.activity.id":"urn:uuid:339f337a-8848-41ec-adba-73da367fa66e"}}
    n
    ```
!!! Note
    
    1. There are some limitations in the Jaeger client, which by default uses a UDP sender as mentioned in [the Jaeger documentation](https://www.jaegertracing.io/docs/1.22/client-libraries/). If the payload size exceeds 65 KB, spans might get lost in the Jaeger console. 
    2. Jaeger [sampler types](https://www.jaegertracing.io/docs/1.22/sampling/) can also play a major role in tracing. Depending on the TPS, the sampler type should be carefully chosen.
    3. In general, before including tracing in production deployments it is essential to look into performance tests and scaling requirements. Refer the [Jaeger performance tuning guide](https://www.jaegertracing.io/docs/1.22/performance-tuning/) for details on how to achieve better performance. 

## Use Custom Tracer Implementation

In order to demonstrate this functionality, let's take a scenario with the implementation of Elastic APM (Application Performance Monitoring).

1. Implement the `org.wso2.carbon.apimgt.tracing.OpenTracer` interface and add your implementation. The getTracer method should contain the generation of the `Tracer` instance. Also, the getName method should return the tracer name to be configured in the `deployment.toml` file. In this specific scenario we are naming this tracer `elastic`. This tracer needs to be loaded as an osgi service using a module activator. The sample project for the elastic APM tracer can be downloaded from [here]({{base_path}}/assets/attachments/administer/custom.tracing.client.zip).

2. Build the maven project and add the jar file to the dropins directory. (API-M_HOME/repository/components/dropins)

3. Add the following configuration into the `deployment.toml` file.

    ```toml tab="Format"
    [apim.open_tracer]
    remote_tracer.enable = true
    remote_tracer.name = <custom_tracer_name>
    ```

    ```toml tab="Example"
    [apim.open_tracer]
    remote_tracer.enable = true
    remote_tracer.name = "elastic"
    ```

4. Add the elastic opentracer jar file to the lib directory (API-M_HOME/repository/components/lib). It can be downloaded from [here](https://mvnrepository.com/artifact/co.elastic.apm/apm-opentracing). 

    !!! tip
        Elastic opentracing also requires the addition of a java agent. This can be added by altering the startup script. Make sure to check the documentation for the tracer you are using so that such requirements can be satisfied. 

5. Start the server.

     After you invoke the APIs tracing data will be published to elastic APM

    [![Distributed tracing elastic]({{base_path}}/assets/img/administer/elastic-tracer.png)]({{base_path}}/assets/img/administer/elastic-tracer.png)