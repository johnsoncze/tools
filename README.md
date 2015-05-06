# PgSQL
## Depth in tree
```
  SELECT (SELECT COUNT(*) FROM (
    WITH RECURSIVE tree AS (
      SELECT id, ARRAY[]::INTEGER[] AS ancestors
      FROM admin.navigation AS nodes WHERE parent_id IS NULL

      UNION ALL

      SELECT nodes.id, tree.ancestors || nodes.parent_id
      FROM admin.navigation AS nodes, tree
      WHERE nodes.parent_id = tree.id
    ) SELECT UNNEST(ancestors) FROM tree WHERE id = navigation.id
  ) AS "ancestors") AS "depth"
```