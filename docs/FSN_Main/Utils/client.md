---
sort: 1
---

# Client Utils
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
