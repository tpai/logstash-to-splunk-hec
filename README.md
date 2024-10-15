# Logstash to Splunk HEC

This project is to demo how to use HTTP Event Collector(HEC) to send logs from Logstash to Splunk.

## API Testing Call

```bash
# cURL -> Splunk
curl -k https://localhost:8088/services/collector/event \
    -H "Authorization: Splunk splunkhectoken" \
    -d '{"event": "hello from cURL"}'

# cURL -> Logstash -> Splunk
curl http://localhost:5044 \
    -H "Content-Type: application/json" \
    -d '{"message": "hello from logstash", "level": "info", "@timestamp": "2024-10-15T12:00:00"}'
```

## Dev Mode

1. Start server
    ```bash
    SPLUNK_PASSWORD=password docker-compose up -d
    ```
1. Configure HEC: Settings > Data Inputs > HTTP Event Collector
1. Set default index to `main`
1. Navigate to search: Apps > Search & Reporting
1. Call API
1. Search logs with query: `(index="main")`
1. Make changes on pipeline config `logstash.conf`
1. Wait 5s until logstash auto-reload
1. Back to step 5
