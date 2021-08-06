---
sort: 1
---
# Items and Stores
Items are stored in the `sv_presets.lua` to avoid database calls to things that are static. Items need to be added to the file following the same format of the other items. Item uses can be defined in a couple ways but the easiest is to add the use of the item to `cl_uses.lua`

## Adding an Item
To add an item to your server open up the `sv_presets.lua` and use the following  format to add said item:

```lua
	["indexname"] = { -- index of the item in the item table. Case sensitive. Typically named the same as the index field below. this is the name you would use to add items to your inventory
		index = 'bandage', -- Name of the item. This needs to match the image name in htl/img/items
		name = 'Bandage', -- Visual name of the item. How it will show in your inventory, stash, etc
		data = {
			weight = 0.4 -- Weight of the item
		},
	},
```

If you are adding a weapon then you need to follow the weapon item style which is:

```lua
    ['weapon_pumpshotgun'] = { -- index of the item in the item table. Case sensitive Typically named the same as the index field below. this is the name you would use to add items to your inventory
        index = "weapon_pumpshotgun", -- name of the weapon. . This should be the same name as the MODEL of the weapon you want to add. like weapon_pistol or weapon_pumpshotgun. This name also has to match the image name in html/img/items
        name = "Pump Shotgun", -- The name of the item as it is displayed in the inventory, stash, etc
        amt = 1, -- Amount to stack. Should generally stay at 1
        customData = {
            weapon = 'true', -- Is this a weapon? true/false
            ammo = 200, -- How much ammo the weapon will come with when bought from a store
            ammotype = '12gauge_ammo', -- what type of ammo the weapon uses
            quality = 'normal' -- the type of quality the weapon is. Right now this does nothing
        }
    },

    -- Example of a weapon that does not have ammo and ammoType defined.
    ['petrolcan'] = {
		index = "weapon_petrolcan",
		name = 'Gas Can',
		amt = 1,
        customData = {
            weapon = 'true',
            ammo = 0,
            ammotype = 'none',
            quality = 'perfect'
        }
	},

```

```tip
Generally copying a previous item and pasting will make sure you get all the data you need to create an item just be sure to change the name and remember it is case sensitive. Also make sure you include the trailing `,` after the last `}` otherwise your file will fail to load and be sure you actually put the item inside the presetItems table that is defined. (Before line 536)
```

## Adding an item image
Item images are located under `fsn_inventory/html/img/items`

You can use an existing image for reference on size of the picture and quality. The image **MUST** be a PNG in order to load. The name also has to match the index name of the item that you set in `sv_presets.lua`

```tip
The `__resource.lua` is already set up with a wildcard to load all the images located in the directory.
```
## Item Uses
Item uses can be defined either by triggereing an event when you use the item or by actually defining the use under `fsn_inventory/cl_uses.lua`

Following the format you can add unique uses to every item. A couple of examples are:

```lua
	["scuba"] = { -- match the ['scuba'] from sv_presets.lua
		takeItem = true, -- Want to take the item on use? true/false
		use = function(item) -- here is where you define what this item will do. Everythiong after this line will be triggered on item use
			TriggerEvent('fsn_inventory:rebreather:use') -- for example this will trigger the event and put on scuba gear on your character
		end,
	},

    -- Use of the id. Little more advanced than the above item use but still pretty simple. Same format
	["id"] = { -- match the ['id'] from sv_presets.lua
		takeItem = false, -- Want to take the item on use? true/false
		use = function(item) -- Defining what the item will do on use. Everything after this line is what is triggered when the item is used
			local players = {} -- creates a players table
			for _, ply in pairs(GetActivePlayers()) do -- gets Active Players
                local playerCoords = GetEntityCoords(PlayerPedId())
                local otherPlayerCoords = GetEntityCoords(GetPlayerPed(ply))
				if #(otherPlayerCoords.xyz - playerCoords.xyz) < 5.0 then -- Checks the distance and if it is less than 5.0 will add all surrounding players to the player table created above
					players[#players+1] = GetPlayerServerId(ply)
				end
			end
			TriggerServerEvent('fsn_licenses:id:display', players, item.customData.Name, item.customData.Occupation, item.customData.DOB, item.customData.Issue, item.customData.CharID) -- triggers the event to display the license in chat to only the surrounding players
		end,
	},

    -- Use of the bandage. Alot more triggers here but again fairly simple and same format
    ["bandage"] = {
		takeItem = true,
		use = function(item)
			TriggerEvent('mythic_hospital:client:RemoveBleed')
			TriggerEvent('fsn_ems:ad:stopBleeding')
			TriggerEvent('fsn_evidence:ped:addState', 'Has bandage', 'UPPER_BODY', 20)
			if GetEntityHealth(GetPlayerPed(-1)) < 131 then
				TriggerEvent('fsn_inventory:item:take', 'bandage', 1)
				while ( not HasAnimDictLoaded( "oddjobs@assassinate@guard" ) ) do
					RequestAnimDict( "oddjobs@assassinate@guard" )
					Citizen.Wait( 5 )
				end
				TaskPlayAnim(GetPlayerPed(-1), "oddjobs@assassinate@guard", "unarmed_fold_arms", 8.0, 1.0, 2500, 2, 0, 0, 0, 0 )  
				Citizen.Wait(1500)
				SetEntityHealth(GetPlayerPed(-1), GetEntityHealth(GetPlayerPed(-1))+15)
			else
				TriggerEvent('fsn_notify:displayNotification', 'You don\'t need to use a bandage!<br>Visit an EMS personnel or a hospital to heal more.', 'centerLeft', 3500, 'error')
			end
		end
	},
```

## Adding items to a store
Store's stock can be found under `fsn_store/server.lua`. You can use an existing item to see how the format is applied to add stock to a store. A few examples are:

```lua
    ['liquorace'] = { -- name of the store also defined in client.lua
      busy = false, -- If the store is busy. this should always be false. otherwise you would never be able to open the store
      stock = { -- here is the start of the stock table
        beef_jerky        = { amt = 999, price = 4}, -- should be pretty self explanatory. the name should match the ['itemname'] in sv_presets.lua amt is the amount of the item the store will have in stock. price is the price of the item. Dont forget the trailing , when adding items.
        cupcake           = { amt = 999, price = 1},
        microwave_burrito = { amt = 999, price = 8},
        panini            = { amt = 999, price = 6},
        pepsi             = { amt = 999, price = 5},
        phone             = { amt = 999, price = 250},
        bandage           = { amt = 1500, price = 250},
        binoculars        = { amt = 999, price = 250}

      }
    },

    -- gunstore example
    ['ammunation'] = {
		busy = false,
		stock = {
		  weapon_combatpistol 	  	= { amt = 9999, price = 500},
		  weapon_smg 			    = { amt = 9999, price = 500},
		  weapon_fireextinguisher 	= { amt = 9999, price = 500},
		  ammop			            = { amt = 9999, price = 600},
		  ammosmg 			        = { amt = 9999, price = 600},
		  --armor 			        = { amt = 9999, price = 1000},
		}
	  },
```

## Adding a new store
Stores can be added under `fsn_store` in both the `client.lua` and the `server.lua`. When adding a store be sure to follow the same format as the default stores and be sure the names match on both server and client side. Examples:

Client Side:
```lua
	--[[ To go over what each field does:
		id: this is the id of the store. This is case sensitive and NEEDS to match the index on the serve side. This should always be in '' and be a string
		xyz: the vector coordinates of where the store is located
		blip: true/false. determines whether a blip will be displayed on the map or not
		busy: false. This should ALWAYS be false
		gunstore: true/false this will determine if the store is a gunstore or not
	]]
  	{id = 'twentyfourseven', xyz = vector3(1730.2172851563, 6415.9599609375, 35.037227630615), blip=true, busy = false, gunstore = false},
  	{id = 'twentyfourseven', xyz = vector3(2678.9938964844, 3281.0151367188, 55.241138458252), blip=true, busy = false, gunstore = false},
  	{id = 'twentyfourseven', xyz = vector3(2557.4074707031, 382.74633789063, 108.62294769287), blip=true, busy = false, gunstore = false},

	{id = 'pillbox', xyz = vector3(316.72573852539, -588.17431640625, 43.291801452637), blip=false, busy = false, gunstore = false},

	{id='ammunation', xyz = vector3(20.658050537109, -1106.4268798828, 29.797029495239), blip=true, busy = false, gunstore = true},
	{id='dark_market', xyz = vector3(252.50720214844, -48.169807434082, 69.941047668457), blip=false, busy = false, gunstore = true},

```

Server Side:
```lua
	--[[
		[''] this is the store index in the stores table this needs to match the id on the client side
		busy: should always be false
		stock: the stores stock of items
	]]

    ['twentyfourseven'] = {
      busy = false,
      stock = {
        beef_jerky        = {amt=999,price=4},
        cupcake           = {amt = 999, price = 1},
        microwave_burrito = {amt = 999, price = 8},
        panini            = {amt = 999, price = 6},
        pepsi             = {amt = 999, price = 5},
        phone             = {amt = 999, price = 250},
        bandage           = {amt = 1500, price = 250},
        binoculars        = {amt = 999, price = 250}

      }
    },

    ['pillbox'] = {
      busy = false,
      stock = {
        beef_jerky        = { amt = 999, price = 4},
        cupcake           = { amt = 999, price = 1},
        microwave_burrito = { amt = 999, price = 8},
        panini            = { amt = 999, price = 6},
        pepsi             = { amt = 999, price = 5},
        phone             = { amt = 999, price = 250},
        bandage           = { amt = 1500, price = 250},
        binoculars        = { amt = 999, price = 250}

      }
    },

	['ammunation'] = {
      busy = false,
      stock = {
        weapon_assaultrifle   		= {amt = 999, price = 10000},
        weapon_combatpistol 	  	= {amt = 999, price = 500},
        weapon_smg 			      	= {amt = 999, price = 500},
        weapon_fireextinguisher 	= {amt = 999, price = 500},
        ammo_pistol 			    = {amt = 999, price = 600},
        ammo_pistol_large 		  	= {amt = 999, price = 800},
        ammo_smg 				    = {amt = 999, price = 600},
        ammo_smg_large 			    = {amt = 999, price = 800},
      }
    },

	['dark_market'] = {
      busy = false,
      stock = {
        weapon_assaultrifle   		= {amt = 999, price = 10000},
        weapon_combatpistol 	  	= {amt = 999, price = 500},
        weapon_smg 			      	= {amt = 999, price = 500},
        ammo_smg 				    = {amt = 999, price = 600},
        ammo_smg_large 			    = {amt = 999, price = 800},
        armor 					    = {amt = 999, price = 1000},
      }
    },
```