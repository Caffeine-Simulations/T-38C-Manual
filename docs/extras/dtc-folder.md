# External DTC Folder
The first time you spawn in the T-38C, several files will be generated in the `Saved Games/DCS_T38C` directory. These files allow a the user to configure a preset database to standardise the configuration of the jet each time you load in. 

For Virtual Squadrons, your instructor pilots will be able to create preset databases for your servers, then send them out to your students, allowing you to build a curriculum of sorties, with minimal effort.

!!! Warning
    The first time you load into the jet on a new map, it will also generate new sub folders for each datatype. This will produce warnings in the top right corner, but they can be safely ignored.

## Folder Structure
File paths of the folders.  
`<Map Name>` will be substituted with `Nevada` or `MarianaIslands` etc. depending on the map currently in use.

**DEST Point Database:**  
`DEST-FPL DATABASE/<Map Name>/DEST.lua`  
**Flight Plan Database:**  
`DEST-FPL DATABASE/<Map Name>/FPL.lua` TODO this isn't implemented, remove when needed  
**ICAO Database:**  
`ICAO DATABASE/<Map Name>/ICAO.lua`  
**Training Zone Database:**  
`Training Zones/<Map Name>/ZONES.lua`  TODO no fly zones???  
**DTC.lua**  
`DTC.lua`  
**TCAS.lua**  
`TCAS.lua`

---

## DEST Point Database

Creating a `DEST-FPL DATABASE/<Map Name>/DEST.lua` file using the data below will allow you to add custom predefined waypoints. To add a new waypoint, copy the template below, and edit the number inside the square brackets (Waypoint 001 can be set using `[1]` etc).

Make sure to follow the DEST database conventions in the table here. TODO link to table with DEST points

```lua
local DEST_TABLE = {
    -- 0/000 cannot be set, since it is the EGI align point
    -- 1 == 001, this conversion happens automatically
    -- 611-649 also cannot be set, as per the real jet
    [13] = {
        ["lat"] = 36.38759,
        ["lon"] = -115.34516,
        ["alt"] = 1568
    },
    [599] = {
        ["lat"] = 36.58391,
        ["lon"] = -115.67235,
        ["alt"] = 1254
    },
}

-- these must be present, leave them at the bottom of the file
local function get_dest_table()
    return DEST_TABLE
end

return {
    get_dest_table = get_dest_table,
}
```

!!! Warning
    Do not set point 0 (000) as this is set automatically when you load in/align the EGI  
    Waypoints 611-649 are not supported by the jet, use other numbers.
---

## Flight Plan Database
TODO, implementation needed

---

## ICAO Point Database

TODO
!!! Note
    DM Hayds_93 on discord about customizing this
---

## Training Zone Database 
Creating a `TRAINING ZONES/<Map Name>/ZONES.lua` file allows for the creation of real world training zones. Either create a table yourself, or use a tool such as ChatGPT to convert the data into the required format.

!!! Note
    Training Zones can also be configured in the mission editor TODO add link

You can enter coordinates in any of the formats listed at the top of the file, then specify the format you have used into the `format` field. This will tell the jet which converter is needed to convert the data into DCS's coordinate system. The drawing of the zones will happen automatically from there.

```lua
local format = {
    ["DECIMAL"] = 1,
    ["DMM"] = 2,
    -- TODO add more formats, they need a corresponding conversion function in mdp_ZONE_database.lua
}


local zones = {
    [1] = {
        name    = "ATCAA1",     -- This will show up in the Zone page
        enabled = true,         -- This toggles whether it will be enabled by default
        format = format.DMM,    -- Used to determine how to convert the values below
        points  = {             -- The corners of the zones
            [1] = { lat = 1250.0, lon = 14510.0 },
            [2] = { lat = 1125.0, lon = 14700.0 },
            [3] = { lat = 1030.0, lon = 14700.0 },
            [4] = { lat = 1030.0, lon = 14520.0 },
            [5] = { lat = 1250.0, lon = 14500.0 },
            [6] = { lat = 1250.0, lon = 14510.0 },
        },
    },

    [2] = {                     -- Repeat for as many zones as required
        name    = "ATCAA2",
        enabled = true,
        format = format.DMM,    -- You can have different formats for each zone
        points  = {
            [1] = { lat = 1250.0, lon = 14410.0 },
            [2] = { lat = 1250.0, lon = 14440.0 },
            [3] = { lat = 1030.0, lon = 14455.0 },
            [4] = { lat = 1030.0, lon = 14300.0 },
            [5] = { lat = 1220.0, lon = 14200.0 },
            [6] = { lat = 1250.0, lon = 14410.0 },
        },
    },
}

-- leave these lines untouched
local function getZones()
    return zones
end

return {
    getZones = getZones,
}
```
!!! Warning
    Setting the wrong format will cause the lines to not be visible, although the zones will show up on the ZONE page.

---

## DTC.lua
DTC.lua allows you to configure various settings automatically, Such as which HUD mode is default, Callsign, Warning modes, and various other configurable settings. This only changes the defaults, all values can still be changed using the UFCP.

Editing the DTC.lua is very basic, simply find the values you want to change, and follow the instructions in the comments. 

!!! Warning
    ONLY change the value after the equals (=).

!!! Note
    If you make an error, and the DTC.lua fails to load, simply delete the file and reload the jet, a new working file will be generated, this will be verified by a warning in the top right of the screen

```lua
-- here is an example DTC.lua TODO flesh this out later in the process
local DTCData = {
    ["settings"] = { -- format: [param_handle_name] = value
        ["ADSB_CALLSIGN"] = "ASPEN11", -- Callsign for ADS-B. max of 7 characters (e.g. ASPEN11)
        ["SQUAWK"] = 1234,
        -- TODO add VFR and EMERGENCY squawks here, these need to be set in the device too
        ["DDS_MODE"] = 2, -- (HOTAS Button behaviour for PFR Swapping) 0 = HSD, 1 = SIT, 2 = BTH
        -- TODO CDM Mode here
        ["ALT_WARN_MODE"] = 0, -- (Altitude Warning Mode) 0 = "BOTH", 1 = "MSL", 2 = "RALT", 3 = "OFF"}
        ["ALT_WARN_MSL"] = 6000, -- last digit must be 0, between 0 and 50000
        ["ALT_WARN_RAD"] = 250, -- last digit must be 0, between 0 and 5000
        ["HUD_MODE"] = 0,       -- 0 = F-16, 1 = MIL-STD
        -- TODO other hud page stuff
    }
}
```

---

## TCAS.lua
The TCAS in our T-38C works on the assumption that planes the user adds to this file have ADSB/Mode C out on at all times. Customize this list to change the behaviour of what will show up when TCAS TA/RA is selected.

The `TCAS.lua` file is generated automatically with a premade database. this file is used to filter which planes show up on TCAS. This allows for you to add your own, or other mods, although we will try to add as many as possible.

Offical module names can be found [here](https://github.com/pschiel/opsdcs/blob/main/opsdcs-setup/dcs-module-names.md){:target="_blank"}.

```lua
local TCAS = {
    "T-38C",
    "T-38A",
    "F-15ESE",
    "F-15C",
    "F-16C_50",
    "A-10C_2",
    "CH-47Fbl1",
    -- Add more planes here
}

-- Leave these untouched
local function loadTCAS()
    return TCAS
end

return {
    loadTCAS = loadTCAS
}
```

---
