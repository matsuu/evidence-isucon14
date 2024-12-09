---
title: Score
---

```sql scores
SELECT *, 'https://github.com/matsuu/isucon14f/commit/' || hash AS github, substring(hash, 1, 7) AS short FROM isucon14.reports ORDER BY id;
```

<LineChart data={scores} x=created_at y=score xFmt="YYYY-MM-DD hh:mm:ss">
  <ReferenceArea xMin="2024-12-08 10:00:00" xMax="2024-12-08 18:00:00" label="本番" />
  <ReferenceArea xMin="2024-12-09 16:00:00" xMax="2024-12-16 16:00:00" label="感想戦" color=green />
  <ReferenceLine y=58153 label="本番1位スコア" color=red />
</LineChart>

<DataTable data={scores} rows=100>
  <Column id=id />
  <Column id=created_at fmt="YYYY-MM-DD hh:mm:ss" />
  <Column id=score fmt=num0 />
  <Column id=github contentType=link linkLabel=short title=Commit />
  <Column id=comment />
</DataTable>
