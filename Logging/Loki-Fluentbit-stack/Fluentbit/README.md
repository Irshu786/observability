## Basic FluentBit conf for enabling logs from k8s nodes to Loki


[SERVICE]
    Flush        {{ .Values.flush }}
    Daemon       Off
    Log_Level    info
    HTTP_Server on
    HTTP_Listen 0.0.0.0
    Health_Check On
[INPUT]
    Name         tail
    Path         /var/log/containers/*.log
    Tag          kube.*
    Skip_Empty_Lines On
    
[FILTER]
    Name         kubernetes
    Match        kube.*
    K8S-Logging.Parser On

[OUTPUT]
    Name         loki
    Match        kube.*
    Host         loki-gateway.loki.svc.cluster.local
    Port         80
    URI          /loki/api/v1/push
    Labels       job="fluentbit"
    auto_kubernetes_labels On
    line_format   json
