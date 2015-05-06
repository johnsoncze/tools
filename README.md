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

# Sublime
## Settings
```
  {
    "color_scheme": "Packages/User/Flatland Dark (SL).tmTheme",
    "convert_tabspaces_on_save": true,
    "draw_white_space": "all",
    "flatland_sidebar_tree_xsmall": true,
    "flatland_square_tabs": true,
    "font_size": 11,
    "ignored_packages":
    [
      "Vintage",
      "Theme - Flatland",
      "SublimeLinter"
    ],
    "tab_size": 2,
    "theme": "Soda Light 3.sublime-theme",
    "translate_tabs_to_spaces": true,
    "trim_trailing_white_space_on_save": true
  }
```