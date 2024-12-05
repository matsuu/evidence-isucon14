---
title: Score
---

```sql scores
SELECT * FROM isucon14.reports ORDER BY id;
```

<LineChart data={scores} x=created_at y=score />

<DataTable data={scores}>
  <Column id=id />
  <Column id=created_at fmt="hh:mm:ss" />
  <Column id=score contentType=colorscale />
  <Column id=hash />
  <Column id=comment />
</DataTable>
