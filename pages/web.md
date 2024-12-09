---
title: web
---

```sql reports
SELECT id, format('{} | {:d} | {}', strftime(created_at, '%Y-%m-%d %H:%M:%S'), score::INTEGER, comment) AS label FROM isucon14.reports ORDER BY id DESC;
```

<Dropdown data={reports} name=report_id value=id label=label title=対象 order="id desc" />

<Checkbox title="initializeを除く" name=without_initialize defaultValue=true />

# By Count

リクエスト毎の回数とステータスコード

```sql web_by_count
SELECT * EXCLUDE(report_id) FROM isucon14.web_by_count WHERE report_id = ${inputs.report_id.value} AND (NOT ${inputs.without_initialize} OR Pattern NOT LIKE '%initialize%') ORDER BY cnt DESC;
```

<DataTable data={web_by_count} rows=50 search=true>
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

リクエスト毎の応答時間

```sql web_by_latency
SELECT * EXCLUDE(report_id) FROM isucon14.web_by_latency WHERE report_id = ${inputs.report_id.value} AND (NOT ${inputs.without_initialize} OR Pattern NOT LIKE '%initialize%')
```

<DataTable data={web_by_latency} rows=50 search=true>
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

リクエスト毎のアップロード量

```sql web_by_upload_bytes
SELECT * EXCLUDE(report_id) FROM isucon14.web_by_upload_bytes WHERE report_id = ${inputs.report_id.value} AND (NOT ${inputs.without_initialize} OR Pattern NOT LIKE '%initialize%');
```

<DataTable data={web_by_upload_bytes} rows=50 search=true>
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

リクエスト毎のダウンロード量

```sql web_by_download_bytes
SELECT * EXCLUDE(report_id) FROM isucon14.web_by_download_bytes WHERE report_id = ${inputs.report_id.value} AND (NOT ${inputs.without_initialize} OR Pattern NOT LIKE '%initialize%');
```

<DataTable data={web_by_download_bytes} rows=50 search=true>
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

プロトコルランキング

```sql web_top_protocols
SELECT * EXCLUDE(report_id) FROM isucon14.web_top_protocols WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_top_protocols} rows=50 search=true rowNumbers=true>
  <Column id=cnt contentType=bar />
  <Column id=Protocol />
</DataTable>

# Top RemoteAddr

接続元ランキング

```sql web_top_remoteaddr
SELECT * EXCLUDE(report_id) FROM isucon14.web_top_remoteaddr WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_top_remoteaddr} rows=50 search=true rowNumbers=true>
  <Column id=cnt contentType=bar />
  <Column id=RemoteAddr />
</DataTable>

# Top Host

Hostヘッダーランキング

```sql web_top_host
SELECT * EXCLUDE(report_id) FROM isucon14.web_top_host WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_top_host} rows=50 search=true rowNumbers=true>
  <Column id=cnt contentType=bar />
  <Column id=Host />
</DataTable>

# Top Method

リクエストメソッドランキング

```sql web_top_method
SELECT * EXCLUDE(report_id) FROM isucon14.web_top_method WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_top_method} rows=50 search=true rowNumbers=true>
  <Column id=cnt contentType=bar />
  <Column id=Method />
</DataTable>

# Top Status

ステータスコードランキング

```sql web_top_status
SELECT * EXCLUDE(report_id) FROM isucon14.web_top_status WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_top_status} rows=50 search=true rowNumbers=true>
  <Column id=cnt contentType=bar />
  <Column id=Status />
</DataTable>

# Top Latency

応答時間ランキング

```sql web_top_latency
SELECT * EXCLUDE(report_id) FROM isucon14.web_top_latency WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_top_latency} rows=50 search=true compact=true rowNumbers=true>
  <Column id=rank />
  <Column id=Latency contentType=bar />
  <Column id=Method />
  <Column id=Host />
  <Column id=URL title=Path />
</DataTable>

# Top SSL

SSLランキング

```sql web_top_ssl
SELECT cnt,* EXCLUDE(cnt,report_id) FROM isucon14.web_top_ssl WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_top_ssl} rows=50 search=true>
</DataTable>

# Request Headers

リクエスト毎のリクエストヘッダーパターン

```sql web_request_headers
SELECT Method || ' ' || Pattern AS request, headers, cnt FROM isucon14.web_request_headers WHERE report_id = ${inputs.report_id.value} AND (NOT ${inputs.without_initialize} OR Pattern NOT LIKE '%initialize%') ORDER BY Pattern, Method;
```

<DataTable data={web_request_headers} rows=50 groupBy=request accordionRowColor=#f2f2f2 search=true>
  <Column id=headers />
  <Column id=cnt contentType=colorscale />
</DataTable>

# Request Headers Analysis

リクエストヘッダーの利用回数、ユニーク回数、エントロピー、最頻値

```sql web_request_headers_analysis
SELECT * EXCLUDE(report_id) FROM isucon14.web_request_headers_analysis WHERE report_id = ${inputs.report_id.value};
```

<DataTable data={web_request_headers_analysis} rows=50 search=true>
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
  yAxisTitle="セッション数"
  yGridlines=false
  xBaseline=false
/>

# Response Headers

リクエスト毎のレスポンスヘッダーパターン

```sql web_response_headers
SELECT Method || ' ' || Pattern AS request, headers, cnt FROM isucon14.web_response_headers WHERE report_id = ${inputs.report_id.value} AND (NOT ${inputs.without_initialize} OR Pattern NOT LIKE '%initialize%') ORDER BY Pattern, Method;
```

<DataTable data={web_response_headers} rows=50 groupBy=request accordionRowColor=#f2f2f2 search=true>
  <Column id=headers />
  <Column id=cnt contentType=colorscale />
</DataTable>

# Response Headers Analysis

レスポンスヘッダーの利用回数、ユニーク回数、エントロピー、最頻値

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

ステータスコードが400以上

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
