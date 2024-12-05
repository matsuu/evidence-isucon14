---
title: web
---

```sql reports
SELECT id, format('{} | {:d} | {}', strftime(created_at, '%H:%M:%S'), score::INTEGER, comment) AS label FROM isucon14.reports ORDER BY id DESC;
```

<Dropdown data={reports} name=report_id value=id label=label title=対象 />

# By Count

```sql web_by_count
SELECT cnt/sum(cnt) OVER () AS 'cnt_pct', * EXCLUDE(report_id) FROM isucon14.web_by_count WHERE report_id = ${inputs.report_id.value} ORDER BY cnt DESC;
```

<DataTable data={web_by_count} rows=50 search=true>
  <Column id=cnt_pct title="Cnt%" contentType=colorscale />
  <Column id=cnt contentType=colorscale />
  <Column id=1xx contentType=colorscale />
  <Column id=2xx contentType=colorscale />
  <Column id=3xx contentType=colorscale />
  <Column id=4xx contentType=colorscale />
  <Column id=5xx contentType=colorscale />
  <Column id=other contentType=colorscale />
  <Column id=Method />
  <Column id=Pattern />
</DataTable>

# By Latency

```sql web_by_latency
SELECT Sum/sum(Sum) OVER () AS sum_pct, * EXCLUDE(report_id) FROM isucon14.web_by_latency WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_by_latency} rows=50 search=true>
  <Column id=sum_pct title="Sum%" contentType=colorscale />
  <Column id=cnt contentType=colorscale />
  <Column id=sum contentType=colorscale />
  <Column id=min contentType=colorscale />
  <Column id=avg contentType=colorscale />
  <Column id=p50 contentType=colorscale />
  <Column id=p99 contentType=colorscale />
  <Column id=max contentType=colorscale />
  <Column id=Method />
  <Column id=Pattern />
</DataTable>

# By Upload Bytes

```sql web_by_upload_bytes
SELECT Sum/sum(Sum) OVER () AS sum_pct, * EXCLUDE(report_id) FROM isucon14.web_by_upload_bytes WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_by_upload_bytes} rows=50 search=true>
  <Column id=sum_pct title="Sum%" contentType=colorscale />
  <Column id=cnt contentType=colorscale />
  <Column id=sum contentType=colorscale />
  <Column id=min contentType=colorscale />
  <Column id=avg contentType=colorscale />
  <Column id=p50 contentType=colorscale />
  <Column id=p99 contentType=colorscale />
  <Column id=max contentType=colorscale />
  <Column id=Method />
  <Column id=Pattern />
</DataTable>

# By Download Bytes

```sql web_by_download_bytes
SELECT Sum/sum(Sum) OVER () AS sum_pct, * EXCLUDE(report_id) FROM isucon14.web_by_download_bytes WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_by_download_bytes} rows=50 search=true>
  <Column id=sum_pct title="Sum%" contentType=colorscale />
  <Column id=cnt contentType=colorscale />
  <Column id=sum contentType=colorscale />
  <Column id=min contentType=colorscale />
  <Column id=avg contentType=colorscale />
  <Column id=p50 contentType=colorscale />
  <Column id=p99 contentType=colorscale />
  <Column id=max contentType=colorscale />
  <Column id=Method />
  <Column id=Pattern />
</DataTable>

# Top Protocols

```sql web_top_protocols
SELECT cnt/sum(cnt) OVER () AS cnt_pct, * EXCLUDE(report_id) FROM isucon14.web_top_protocols WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_top_protocols} rows=50 search=true rowNumbers=true>
  <Column id=cnt_pct title="Cnt%" contentType=colorscale />
  <Column id=cnt contentType=colorscale />
  <Column id=Protocol />
</DataTable>

# Top RemoteAddr

```sql web_top_remoteaddr
SELECT cnt/sum(cnt) OVER () AS cnt_pct, * EXCLUDE(report_id) FROM isucon14.web_top_remoteaddr WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_top_remoteaddr} rows=50 search=true rowNumbers=true>
  <Column id=cnt_pct title="Cnt%" contentType=colorscale />
  <Column id=cnt contentType=colorscale />
  <Column id=RemoteAddr />
</DataTable>

# Top Host

```sql web_top_host
SELECT cnt/sum(cnt) OVER () AS cnt_pct, * EXCLUDE(report_id) FROM isucon14.web_top_host WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_top_host} rows=50 search=true rowNumbers=true>
  <Column id=cnt_pct title="Cnt%" contentType=colorscale />
  <Column id=cnt contentType=colorscale />
  <Column id=Host />
</DataTable>

# Top Method

```sql web_top_method
SELECT cnt/sum(cnt) OVER () AS cnt_pct, * EXCLUDE(report_id) FROM isucon14.web_top_method WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_top_method} rows=50 search=true rowNumbers=true>
  <Column id=cnt_pct title="Cnt%" contentType=colorscale />
  <Column id=cnt contentType=colorscale />
  <Column id=Method />
</DataTable>

# Top Status

```sql web_top_status
SELECT cnt/sum(cnt) OVER () AS cnt_pct, * EXCLUDE(report_id) FROM isucon14.web_top_status WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_top_status} rows=50 search=true rowNumbers=true>
  <Column id=cnt_pct title="Cnt%" contentType=colorscale />
  <Column id=cnt contentType=colorscale />
  <Column id=Status />
</DataTable>

# Top Latency

```sql web_top_latency
SELECT * EXCLUDE(report_id) FROM isucon14.web_top_latency WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_top_latency} rows=50 search=true compact=true rowNumbers=true>
  <Column id=rank />
  <Column id=Latency contentType=colorscale />
  <Column id=Method />
  <Column id=Host />
  <Column id=URL />
</DataTable>

# Top SSL

```sql web_top_ssl
SELECT * EXCLUDE(report_id) FROM isucon14.web_top_ssl WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_top_ssl} rows=50 search=true>
</DataTable>

# Request Headers

```sql web_request_headers
SELECT * EXCLUDE(report_id) FROM isucon14.web_request_headers WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_request_headers} rows=50 search=true>
  <Column id=cnt contentType=colorscale />
  <Column id=Method />
  <Column id=Pattern />
  <Column id=headers />
</DataTable>

# Request Headers Analysis

```sql web_request_headers_analysis
SELECT * EXCLUDE(report_id) FROM isucon14.web_request_headers_analysis WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_request_headers_analysis} rows=50 search=true>
  <!-- Column id=cum_pct title="Cum%" contentType=colorscale / -->
  <Column id=key />
  <Column id=cnt contentType=colorscale />
  <Column id=uniqCnt contentType=colorscale />
  <Column id=entropy contentType=colorscale />
  <Column id=mode />
</DataTable>

# Cookies Count

セッションごとのリクエスト回数の分布

```sql web_cookies_count
SELECT * EXCLUDE(report_id) FROM isucon14.web_cookies_count WHERE report_id = ${inputs.report_id.value};
```

<Histogram
  data={web_cookies_count}
  x=cnt
  xAxisTitle="リクエスト回数"
/>

# Response Headers

```sql web_response_headers
SELECT * EXCLUDE(report_id) FROM isucon14.web_response_headers WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_response_headers} rows=50 search=true>
  <Column id=cnt contentType=colorscale />
  <Column id=Method />
  <Column id=Pattern />
  <Column id=headers />
</DataTable>

# Response Headers Analysis

```sql web_response_headers_analysis
SELECT * EXCLUDE(report_id) FROM isucon14.web_response_headers_analysis WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_response_headers_analysis} rows=50 search=true>
  <!-- Column id=cum_pct title="Cum%" contentType=colorscale / -->
  <Column id=key />
  <Column id=cnt contentType=colorscale />
  <Column id=uniqCnt contentType=colorscale />
  <Column id=entropy contentType=colorscale />
  <Column id=mode />
</DataTable>

# All Errors

```sql web_all_errors
SELECT * EXCLUDE(report_id) FROM isucon14.web_all_errors WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_all_errors} rows=50 search=true>
  <Column id=StartTime fmt="yyyy-mm-dd hh:mm:ss.000" />
  <Column id=Latency contentType=colorscale />
  <Column id=Status />
  <Column id=Method />
  <Column id=Host />
  <Column id=URL />
  <Column id=Error />
</DataTable>