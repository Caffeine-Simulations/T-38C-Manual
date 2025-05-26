# DTC.lua
DTC.lua allows you to configure various settings automatically, Such as which HUD mode is default, Callsign, Warning modes, and various other configurable settings. This only changes the defaults, all values can still be changed using the UFCP.
Manually Editing DTC.lua
Editing the DTC.lua is very basic, simply find the values you want to change, and follow the instructions in the comments. ONLY change the value after the equals (=).

!!! Note
    If you make an error, and the DTC.lua fails to load, simply delete the file and reload the jet, a new working file will be generated, this will be verified by a warning in the top right of the screen

```lua
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
