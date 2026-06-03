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
INSERT INTO `acore_world`.playercreateinfo_action VALUES (3, 8, 10, 159, 128);
INSERT INTO `acore_world`.playercreateinfo_action VALUES (3, 8, 4, 2481, 0);
```

### Client-side Patch
Place the `Patch-Z.MPQ` in your local WoW client 's Data directory.
