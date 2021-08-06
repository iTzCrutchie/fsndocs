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