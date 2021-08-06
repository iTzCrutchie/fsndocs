---
sort: 1
---

# Client Utils Setup
These are all the utils, their functions and how to use them for client side files on your server. Be sure to include `client_script '@fsn_main/cl_utils.lua'` in your fxmanifest.lua for your resource in order to utilise these utils on your client scripts.

Example of a fxmanifest with the client utils defined:

```lua  
fx_version 'cerulean'
games { 'gta5' }

author 'iTzCrutchie'
description 'Activities for the server'
version '0.0.1'

--[[/	:FSN:	\]]--
client_scripts { 
    '@fsn_main/cl_utils.lua',
}
--[[/	:FSN:	\]]--

client_scripts {

    -- Yoga
    'yoga/client.lua',

}
```
## Client Utils
### Util.Tick
*A simple wrapper for CreateThread + while do*

| Argument | Type | Description |
| :--------: | :----: | :-----------: |
| `f` | function | The function you wish to run |
| `ms` | number | Number of milliseconds to wait at beginning. Defaults to `0`. |
#### Example
```lua
--[[
	This example will display 'Example Text' on the player every tick.
]]--

Util.Tick(function()
	local loc = GetEntityCoords(GetPlayerPed(-1))
	Util.DrawText3D(loc.x, loc.y, loc.z, 'Example text')
end) 
``` 
```javascript
	// This function is not available in javascript.
```