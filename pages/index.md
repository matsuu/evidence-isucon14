---
title: Score
---

```sql scores
SELECT *, 'https://github.com/matsuu/isucon14f/tree/' || hash AS github, substring(hash, 1, 7) AS short FROM isucon14.reports ORDER BY id;
```

<LineChart data={scores} x=created_at y=score xFmt="YYYY-MM-DD hh:mm:ss">
  <ReferenceArea xMin="2024-12-08 19:00:00" xMax="2024-12-09 03:00:00" />
</LineChart>

<DataTable data={scores}>
  <Column id=id />
  <Column id=created_at fmt="YYYY-MM-DD hh:mm:ss" />
  <Column id=score />
  <Column id=github contentType=link linkLabel=short title=Commit />
  <Column id=comment />
</DataTable>
