# mod-dwarf-mage
Playable Dwarf Mages for Azeroth Core

## Install
In your `acore_world` database you will need to insert some data to allow dwarf mages to be created. Back up your database before making any modifications.

```SQL
# Allow Dwarf Mages to be created
INSERT INTO `acore_world`.playercreateinfo VALUES (3, 8, 0, 1, -6240.32, 331.033, 382.758, 6.17716);

# Add default actions to the hotbar
INSERT INTO `acore_world`.playercreateinfo_action VALUES (3, 8, 0, 6603, 0);
INSERT INTO `acore_world`.playercreateinfo_action VALUES (3, 8, 1, 133, 0);
INSERT INTO `acore_world`.playercreateinfo_action VALUES (3, 8, 2, 168, 0);
INSERT INTO `acore_world`.playercreateinfo_action VALUES (3, 8, 3, 2481, 0);
INSERT INTO `acore_world`.playercreateinfo_action VALUES (3, 8, 10, 159, 128);
INSERT INTO `acore_world`.playercreateinfo_action VALUES (3, 8, 11, 4540, 128);

# Find all alliance mage only quests
# Allowable Races Combos:
# 1    - Human only
# 64   - Gnome only
# 68   - Dwarf & Gnome only
# 65   - Human & Gnome only
# 1101 - All alliance races
SELECT q.id, q.LogTitle,
       q.AllowableRaces,
       a.AllowableClasses
FROM quest_template q
JOIN quest_template_addon a ON a.id = q.id
WHERE a.AllowableClasses = 128
  AND q.AllowableRaces IN (1, 64, 68, 65, 1101);

# Fix starting quest to allow dwarves to accept quest to see class trainer
# this assumes that "Glyphic Memorandum" is quest 3114 in your database.
# Verify that this is the correct quest before running this update. Use previous query
# to find quest id.
UPDATE `acore_world`.quest_template SET AllowableRaces = 68 WHERE ID = 3114;
```

### Client-side Patch
Place the `Patch-Z.MPQ` in your local WoW client 's Data directory.
