---
sort: 2
---

# Server Utils Setup
These are all the utils, their functions and how to use them for server side files on your server. Be sure to include `server_script '@fsn_main/sv_utils.lua'` in your fxmanifest.lua for your resource in order to utilise these utils on your server scripts.

Example of a fxmanifest with the server utils defined:

```lua  
fx_version 'cerulean'
games { 'gta5' }

author 'iTzCrutchie'
description 'Activities for the server'
version '0.0.1'

--[[/	:FSN:	\]]--
server_scripts { 
    '@fsn_main/sv_utils.lua',
}
--[[/	:FSN:	\]]--

server_scripts {

    -- Yoga
    'yoga/server.lua',

}
```

## Server Utils
### Util.SplitString
*Split the string into table by seperator.* 

| Argument    | Type     | Description |
| -------     | -------- | ----------- |
| `inputstr`  | string   | String to split up. |
| `sep`       | string   | Numerator to seperate the string by. |

#### Example
```lua
AddEventHandler('chatMessage', function(source, auth, msg)
	local split = Util.SplitString(msg, ' ')
end)
``` 
```javascript
	// This function is not available in javascript.
```
### Util.GetSteamID
*Get the SteamID of the player, will drop the player if they don't have one.* 

| Argument    | Type     | Description |
| -------     | -------- | ----------- |
| `src`       | playerID | Player to get the SteamID of. |

#### Example
```lua
AddEventHandler('chatMessage', function(source, auth, msg)
	print(source..' ('..Util.GetSteamID(source)..') said: '..msg)
end)
``` 
```lua
1 (steam:11000010e0828a9) said: Yo wassup
```
```javascript
	// This function is not available in javascript.
```
### Util.MakeString
*Make a randomly generated string* 

| Argument    | Type     | Description |
| -------     | -------- | ----------- |
| `length`    | number   | Number of characters to create string. |

#### Example
```lua
['WEAPON_STUNGUN'] = {
    index = "WEAPON_STUNGUN",
    name = "Stun Gun",
    amt = 1,
    customData = {
        weapon = 'true',
        ammo = 0,
        ammotype = 'none',
        quality = 'normal',
        PDIssued = Util.MakeString(6)
    }
},
``` 
```javascript
	// This function is not available in javascript.
```