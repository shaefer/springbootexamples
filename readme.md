- micrometer test
- auto-time endpoints and include them all
    - management.endpoints.web.exposure.include=*
    - management.metrics.web.server.auto-time-requests=true
    - http metric won't appear on http://localhost:9001/actuator/metrics until first call is made.
- integration with output still shaky
- Timer dimensions managed in uri
    - http://localhost:9001/actuator/metrics/http.server.requests?tag=uri:/helloworld
    - http://localhost:9001/actuator/metrics/http.server.requests?tag=method:GET
    management.metrics.distribution.percentiles-histogram.http.server.requests=true
    management.metrics.distribution.sla.http.server.requests=1ms,5ms,20ms
        - http://localhost:9001/actuator/metrics/http.server.requests.histogram

prometheus.yml

        scrape_configs:
          # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
          - job_name: 'spring_boot_actuator'
            metrics_path: '/actuator/prometheus'
        
            # metrics_path defaults to '/metrics'
            # scheme defaults to 'http'.
        
            static_configs:
            - targets: ['localhost:9001']