# 自定义监控TLQ(东方通)

监控的主要指标如下
 - 就绪状态的消息数
 - 正在发送状态的消息数
 - 正在接收状态的消息数
 - 等待确认应答状态的消息数
 - 接收应用消息的个数
 - 队列的最大容量
 - TLQ License到期时间

1. 官方下载node_exporter, 并解压启动, 启动的时候添加参数

```
# ./node_exporter --collector.textfile.directory=../prom
```

2.配置Prometheus配置文件, 增加node_expoter节点

```
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"
 
    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.
 
    static_configs:
      - targets: ["localhost:9090", "localhost:9100"]
```

最后生成的示例数据如下
```
# HELP tlq_queueh_ready_quantity 就绪状态的消息数
# TYPE tlq_queueh_ready_quantity gauge
tlq_queueh_ready_quantity 0
# HELP tlq_queueh_sdning_quantity 正在发送状态的消息数
# TYPE tlq_queueh_sdning_quantity gauge
tlq_queueh_sdning_quantity 0
# HELP tlq_queueh_rcving_quantity 正在接收状态的消息数
# TYPE tlq_queueh_rcving_quantity gauge
tlq_queueh_rcving_quantity 0
# HELP tlq_queueh_waitack_quantity 等待确认应答状态的消息数
# TYPE tlq_queueh_waitack_quantity gauge
tlq_queueh_waitack_quantity 0
# HELP tlq_queueh_getor_quantity 接收应用消息的个数
# TYPE tlq_queueh_getor_quantity gauge
tlq_queueh_getor_quantity 1
# HELP tlq_queueh_queue_max_capacity 队列的最大容量
# TYPE tlq_queueh_queue_max_capacity gauge
tlq_queueh_queue_max_capacity 100000
# HELP tlq_expire_remain_days TLQ过期剩余天数
# TYPE tlq_expire_remain_days gauge
tlq_expire_remain_days 78
```
