![kevin-licenseplates](https://user-images.githubusercontent.com/89563654/196052842-b97193b0-6f25-44c9-88ca-9866a017c6ae.jpg)

#I am aware of a problem with storing vehicles with it, dont use until you see this removed.

# Preview https://youtu.be/sFFRNqSRGAg
# Dependencies
- QBCore
- qb-inventory/lj-inventory
- oxmysql

------------------------------------------------------------------------------------

* Add the images from the images file into your inventory html images
* Add the below lines into your qb-core>shared>item.lua at the bottom
```lua
	['licenseplate'] 				 = {['name'] = 'licenseplate', 			  	  	['label'] = 'License Plate', 			['weight'] = 1000, 		['type'] = 'item', 		['image'] = 'licenseplate.png', 			['unique'] = true, 		['useable'] = true, 	['shouldClose'] = true,	   ['combinable'] = nil,   ['description'] = ''},
```

* Navigate to your inventory >server > main.lua around lines 1550-1579 the lines may vary on your inventory you can look for the following snippet
```lua
	elseif itemData["name"] == "markedbills" then
		info.worth = math.random(5000, 10000)
```
* Paste the following snippet below or above it does not matter
```lua
	elseif itemData["name"] == "licenseplate" then
		info.plate = tostring(QBCore.Shared.RandomInt(2) .. QBCore.Shared.RandomStr(2) .. QBCore.Shared.RandomInt(2) .. QBCore.Shared.RandomStr(2))
```
* Navigate to the html > js > app.js and find the following snippet
```lua
	} else if (itemData.name == "driver_license") {
		$(".item-info-title").html("<p>" + itemData.label + "</p>");
		$(".item-info-description").html(
			"<p><strong>First Name: </strong><span>" +
			itemData.info.firstname +
			"</span></p><p><strong>Last Name: </strong><span>" +
			itemData.info.lastname +
			"</span></p><p><strong>Birth Date: </strong><span>" +
			itemData.info.birthdate +
			"</span></p><p><strong>Licenses: </strong><span>" +
			itemData.info.type +
			"</span></p><p style=\"font-size:11px\"><b>Weight: </b>" + itemData.weight + " | <b>Amount: </b> " + itemData.amount + " | <b>Quality: </b> " + "<a style=\"font-size:11px;color:green\">" + Math.floor(itemData.info.quality) + "</a>"
		);
```
* And paste the following below it
```lua
	} else if (itemData.name == "licenseplate") {
		$(".item-info-title").html('<p>' + itemData.label + '</p>')
		$(".item-info-description").html('<p><strong>Plate Number: </strong><span>'+ itemData.info.plate);
```
