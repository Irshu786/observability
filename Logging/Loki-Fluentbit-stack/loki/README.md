## The basic setup of loki stack - simple scalable setup

loki-canary
loki-chunks-cache
loki-compactor
loki-distributor, loki-distributor-headless
loki-gateway
loki-index-gateway, loki-index-gateway-headless
loki-ingestor
loki-ingestor-zone-a-headless
loki-ingestor-zone-b-headless
loki-ingestor-zone-c-headless
loki-memberlist
loki-querier
loki-query-frontend, loki-query-frontend
loki-query-scheduler
loki-results-cache
loki-ruler


-- To nake the setup available with basic checks 

1. Disable auth
362 - { auth_enabled: false }
2. loki_configs to improve performance
ingestion_rate_strategy: local
per_stream_rate_limit: 500M
per_stream_rate_limit_burst: 900M
ingestion_rate_mb: 800
ingestion_burst_size_mb: 900
max_global_streams_per_user: 0
max_line_size: 0

3. UI enabled: true
4. lokiCanary: Kind: Deployment [ If required, keep Daemonset ]
5. enableIPV6: false [ Not required of ipv6 ]



















