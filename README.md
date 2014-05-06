# xls2lua
Convert xls to lua script for game res  
use [python xlrd](https://pypi.python.org/pypi/xlrd)

### example
building.xls  
<table>
    <tr>
        <td>ID</td>
        <td>Name</td>
        <td>UseMoney</td>
        <td>UseFood</td>
        <td>IsInit</td>
        <td>Defense</td>
    </tr>
    <tr>
        <td>int</td>
        <td>string</td>
        <td>int</td>
        <td>int</td>
        <td>boolean</td>
        <td>int</td>
    </tr>
    <tr>
        <td>1</td>
        <td>house</td>
        <td>1000</td>
        <td>123</td>
        <td>TRUE</td>
        <td>100</td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td>123</td>
        <td></td>
        <td></td>
        <td>120</td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td>456</td>
        <td></td>
        <td></td>
        <td>130</td>
    </tr>
    <tr>
        <td>2</td>
        <td>farm</td>
        <td>100</td>
        <td>234</td>
        <td>FALSE</td>
        <td>200</td>
    </tr> 
    <tr>
        <td></td>
        <td></td>
        <td>200</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td>200</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>          
</table>
./xls2lua.py building.xls

### NOTICE:
> The **first row** must be **title**.  
> The **second row** must be **type**(**int**, **string**, **boolean**)  
> The **first column** must be **ID**.  
> The **second column** must be **Name**.  

### LUA SCRIPT
```lua
-- this file is generated by program!
-- don't change it manaully.
-- source file: building.xls
-- created at: Tue May 06 02:41:32 2014


local building = {}


building.TypeMap = {}
local TypeMap = building.TypeMap
TypeMap[2] = "farms"
TypeMap["farms"] = 2
TypeMap[1] = "houses"
TypeMap["houses"] = 1


building.farms = {}
local farms = building.farms

farms[1] = {
	ID = 2,
	Name = "farm",
	UseMoney = 100,
	UseFood = 234,
	IsInit = false,
	Defense = 200,
}

farms[2] = {
	UseMoney = 200,
}

farms[3] = {
	UseMoney = 200,
}

building.houses = {}
local houses = building.houses

houses[1] = {
	ID = 1,
	Name = "house",
	UseMoney = 1000,
	UseFood = 123,
	IsInit = false,
	Defense = 100,
}

houses[2] = {
	UseMoney = 123,
	Defense = 120,
}

houses[3] = {
	UseMoney = 456,
	Defense = 130,
}

building.Type= {}
local Type = building.Type
Type[1] = farms
Type[2] = houses



for i=1, #(building.Type) do
	local item = building.Type[i]
	for j=1, #item do
		item[j].__index = item[j]
		if j < #item then
			setmetatable(item[j+1], item[j])
		end
	end
end


return building

```

### HOW TO USE LUA SCRIPT
```lua
local building = require "building"

print(Building.houses[2].ID)
```
The console will print **1**
