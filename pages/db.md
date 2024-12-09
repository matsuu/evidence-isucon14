---
title: db
---

```sql reports
SELECT id, format('{} | {:d} | {}', strftime(created_at, '%Y-%m-%d %H:%M:%S'), score::INTEGER, comment) AS label FROM isucon14.reports ORDER BY id DESC;
```

<Dropdown data={reports} name=report_id value=id label=label title=対象 order="id desc" />

# Slow Query

```sql db_slow_query
SELECT * EXCLUDE(report_id) FROM isucon14.db_slow_query WHERE report_id = ${inputs.report_id.value} ORDER BY sum DESC;
```

<DataTable data={db_slow_query} rows=50 search=true rowNumbers=true>
  <Column id=cnt contentType=colorscale />
  <Column id=sum contentType=colorscale />
  <Column id=min contentType=colorscale />
  <Column id=avg contentType=colorscale />
  <Column id=max contentType=colorscale />
  <Column id=sumLock contentType=colorscale />
  <Column id=sumRows contentType=colorscale />
  <Column id=avgRows contentType=colorscale />
  <Column id=db />
  <Column id=query />
</DataTable>
