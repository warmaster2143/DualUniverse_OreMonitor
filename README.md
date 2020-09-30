# DualUniverse_OreMonitor
This Lua Script will help you to display your ores onto a screen

# Elements required

- 1 Screen M
- 1 Programing Board
- 4 Item Containers

```ruby
--[[ FUNCTIONS ]]--

function round(number,decimals)
    local power = 100^decimals
    return math.floor((number/1000) * power) / power 
end

--[[ EXPORTED VARIABLES ]]--

local tableName = "T1 Ores Status" --export:
local tableNameFontsize = "15em" --export:
local tableFontSize = "20px" --export:
local tableWidth = "100%" --export:
local tableHeight = "100%" --export:
local BGColor = "#252525" --export: This sets the screen background color
local use_L_or_Kg = 0 --export: Use 1 for L or 0 for Kg

--[[ Bauxite ]]--
local maxBauxite = 1000 --export: This is the maximum mass allowed in container. Update as needed
local weightBauxite = 1.28 --export:

if use_L_or_Kg == 1 then
    massBauxite = round(math.ceil(bauxite.getItemsMass()/weightBauxite),2)
    measurement = "L"
elseif use_L_or_Kg == 0 then  
    massBauxite = round(math.ceil(bauxite.getItemsMass()),2)
    measurement = "Kg"
end

local percentBauxite = math.ceil(((math.ceil((bauxite.getItemsMass()/weightBauxite) - 0.5)/maxBauxite)*100))

--[[ Hematite ]]--
local maxHematite = 1200 --export: This is the maximum mass allowed in container. Update as needed
local weightHematite = 5.04 --export:

if use_L_or_Kg == 1 then
    massHematite = round(math.ceil(hematite.getItemsMass()/weightHematite),2)
    measurement = "L"
elseif use_L_or_Kg == 0 then  
    massHematite = round(math.ceil(hematite.getItemsMass()),2)
    measurement = "Kg"
end

local percentHematite = math.ceil(((math.ceil((hematite.getItemsMass()/weightHematite) - 0.5)/maxHematite)*100))

--[[ Coal ]]--
local maxCoal = 1200 --export: This is the maximum mass allowed in container. Update as needed
local weightCoal = 1.35 --export:

if use_L_or_Kg == 1 then
    massCoal = round(math.ceil(coal.getItemsMass()/weightCoal),2)
    measurement = "L"
elseif use_L_or_Kg == 0 then  
    massCoal = round(math.ceil(coal.getItemsMass()),2)
    measurement = "Kg"
end

local percentCoal = math.ceil(((math.ceil((coal.getItemsMass()/weightCoal) - 0.5)/maxCoal)*100))

--[[ Quartz ]]--
local maxQuartz = 1200 --export: This is the maximum mass allowed in container. Update as needed
local weightQuartz = 2.65 --export:

if use_L_or_Kg == 1 then
    massQuartz = round(math.ceil(quartz.getItemsMass()/weightQuartz),2)
    measurement = "L"
elseif use_L_or_Kg == 0 then  
    massQuartz = round(math.ceil(quartz.getItemsMass()),2)
    measurement = "Kg"
end

local percentQuartz = math.ceil(((math.ceil((quartz.getItemsMass()/weightQuartz) - 0.5)/maxQuartz)*100))

--[[ HTML CODE STARTS HERE ]]--

html = [[
<body>

<div class="bootstrap">
<table
	<tr style="
		width: 100%;
		color: white;
	">
	<th>]]..tableName..[[</th>

	<tr style="
		width: 100%;
		margin-bottom: 25px;
		background-color: white;
		color: black;
	">
		<th>Ore</th>
		<th>Levels</th>
		<th>Total Ore</th>
	<tr>
		<th>Bauxite</th>
		<th>]]..percentBauxite..[[%</th>
		<th>]]..massBauxite..measurement..[[</th>
	</tr>
	<tr>
		<th>Hematite</th>
		<th>]]..percentHematite..[[%</th>
		<th>]]..massHematite..measurement..[[</th>
	</tr>
	<tr>
		<th>Coal</th>
		<th>]]..percentCoal..[[%</th>
		<th>]]..massCoal..measurement..[[</th>
	</tr>
	<tr>
		<th>Quartz</th>
		<th>]]..percentQuartz..[[%</th>
		<th>]]..massQuartz..measurement..[[</th>
	</tr>

</table>

<style>
body {
	background-color: ]]..BGColor..[[;
}
h1 {
  	font-size: ]]..tableNameFontsize..[[;
}
table {
  	width: ]]..tableWidth..[[;
	height: ]]..tableHeight..[[;
}
table, th, td {
  	border: 0.5px solid white;
  	border-collapse: collapse;
}
th, td {
  	padding: 10px;
  	text-align: center;
	font-size: ]]..tableFontSize..[[;
}

</style>

</div>

</body>

]]

--[[ HTML CODE ENDS HERE ]]--

screen.setHTML(html)
```

# Quick Setup
```ruby
{"slots":{"0":{"name":"screen","type":{"events":[],"methods":[]}},"1":{"name":"bauxite","type":{"events":[],"methods":[]}},"2":{"name":"hematite","type":{"events":[],"methods":[]}},"3":{"name":"coal","type":{"events":[],"methods":[]}},"4":{"name":"quartz","type":{"events":[],"methods":[]}},"5":{"name":"slot6","type":{"events":[],"methods":[]}},"6":{"name":"slot7","type":{"events":[],"methods":[]}},"7":{"name":"slot8","type":{"events":[],"methods":[]}},"8":{"name":"slot9","type":{"events":[],"methods":[]}},"9":{"name":"slot10","type":{"events":[],"methods":[]}},"-1":{"name":"unit","type":{"events":[],"methods":[]}},"-2":{"name":"system","type":{"events":[],"methods":[]}},"-3":{"name":"library","type":{"events":[],"methods":[]}}},"handlers":[{"code":"-- Stop Timer\n\nunit.stopTimer(\"screen\")\n\n-- Turn Off Screen\n\nscreen.deactivate()\nscreen.clear()","filter":{"args":[],"signature":"stop()","slotKey":"-1"},"key":"0"},{"code":"-- Start Timer\n\nunit.setTimer(\"screen\",1)\n\n-- Turn On Screen\n\nscreen.activate()","filter":{"args":[],"signature":"start()","slotKey":"-1"},"key":"1"},{"code":"--[[ FUNCTIONS ]]--\n\nfunction round(number,decimals)\n    local power = 100^decimals\n    return math.floor((number/1000) * power) / power \nend\n\n--[[ EXPORTED VARIABLES ]]--\n\nlocal tableName = \"T1 Ores Status\" --export:\nlocal tableNameFontsize = \"15em\" --export:\nlocal tableFontSize = \"20px\" --export:\nlocal tableWidth = \"100%\" --export:\nlocal tableHeight = \"100%\" --export:\nlocal BGColor = \"#252525\" --export: This sets the screen background color\nlocal use_L_or_Kg = 0 --export: Use 1 for L or 0 for Kg\n\n--[[ Bauxite ]]--\nlocal maxBauxite = 1000 --export: This is the maximum mass allowed in container. Update as needed\nlocal weightBauxite = 1.28 --export:\n\nif use_L_or_Kg == 1 then\n    massBauxite = round(math.ceil(bauxite.getItemsMass()/weightBauxite),2)\n    measurement = \"L\"\nelseif use_L_or_Kg == 0 then  \n    massBauxite = round(math.ceil(bauxite.getItemsMass()),2)\n    measurement = \"Kg\"\nend\n\nlocal percentBauxite = math.ceil(((math.ceil((bauxite.getItemsMass()/weightBauxite) - 0.5)/maxBauxite)*100))\n\n--[[ Hematite ]]--\nlocal maxHematite = 1200 --export: This is the maximum mass allowed in container. Update as needed\nlocal weightHematite = 5.04 --export:\n\nif use_L_or_Kg == 1 then\n    massHematite = round(math.ceil(hematite.getItemsMass()/weightHematite),2)\n    measurement = \"L\"\nelseif use_L_or_Kg == 0 then  \n    massHematite = round(math.ceil(hematite.getItemsMass()),2)\n    measurement = \"Kg\"\nend\n\nlocal percentHematite = math.ceil(((math.ceil((hematite.getItemsMass()/weightHematite) - 0.5)/maxHematite)*100))\n\n--[[ Coal ]]--\nlocal maxCoal = 1200 --export: This is the maximum mass allowed in container. Update as needed\nlocal weightCoal = 1.35 --export:\n\nif use_L_or_Kg == 1 then\n    massCoal = round(math.ceil(coal.getItemsMass()/weightCoal),2)\n    measurement = \"L\"\nelseif use_L_or_Kg == 0 then  \n    massCoal = round(math.ceil(coal.getItemsMass()),2)\n    measurement = \"Kg\"\nend\n\nlocal percentCoal = math.ceil(((math.ceil((coal.getItemsMass()/weightCoal) - 0.5)/maxCoal)*100))\n\n--[[ Quartz ]]--\nlocal maxQuartz = 1200 --export: This is the maximum mass allowed in container. Update as needed\nlocal weightQuartz = 2.65 --export:\n\nif use_L_or_Kg == 1 then\n    massQuartz = round(math.ceil(quartz.getItemsMass()/weightQuartz),2)\n    measurement = \"L\"\nelseif use_L_or_Kg == 0 then  \n    massQuartz = round(math.ceil(quartz.getItemsMass()),2)\n    measurement = \"Kg\"\nend\n\nlocal percentQuartz = math.ceil(((math.ceil((quartz.getItemsMass()/weightQuartz) - 0.5)/maxQuartz)*100))\n\n--[[ HTML CODE STARTS HERE ]]--\n\nhtml = [[\n<body>\n\n<div class=\"bootstrap\">\n<table\n\t<tr style=\"\n\t\twidth: 100%;\n\t\tcolor: white;\n\t\">\n\t<th>]]..tableName..[[</th>\n\n\t<tr style=\"\n\t\twidth: 100%;\n\t\tmargin-bottom: 25px;\n\t\tbackground-color: white;\n\t\tcolor: black;\n\t\">\n\t\t<th>Ore</th>\n\t\t<th>Levels</th>\n\t\t<th>Total Ore</th>\n\t<tr>\n\t\t<th>Bauxite</th>\n\t\t<th>]]..percentBauxite..[[%</th>\n\t\t<th>]]..massBauxite..measurement..[[</th>\n\t</tr>\n\t<tr>\n\t\t<th>Hematite</th>\n\t\t<th>]]..percentHematite..[[%</th>\n\t\t<th>]]..massHematite..measurement..[[</th>\n\t</tr>\n\t<tr>\n\t\t<th>Coal</th>\n\t\t<th>]]..percentCoal..[[%</th>\n\t\t<th>]]..massCoal..measurement..[[</th>\n\t</tr>\n\t<tr>\n\t\t<th>Quartz</th>\n\t\t<th>]]..percentQuartz..[[%</th>\n\t\t<th>]]..massQuartz..measurement..[[</th>\n\t</tr>\n\n</table>\n\n<style>\nbody {\n\tbackground-color: ]]..BGColor..[[;\n}\nh1 {\n  \tfont-size: ]]..tableNameFontsize..[[;\n}\ntable {\n  \twidth: ]]..tableWidth..[[;\n\theight: ]]..tableHeight..[[;\n}\ntable, th, td {\n  \tborder: 0.5px solid white;\n  \tborder-collapse: collapse;\n}\nth, td {\n  \tpadding: 10px;\n  \ttext-align: center;\n\tfont-size: ]]..tableFontSize..[[;\n}\n\n</style>\n\n</div>\n\n</body>\n\n]]\n\n--[[ HTML CODE ENDS HERE ]]--\n\nscreen.setHTML(html)","filter":{"args":[{"value":"screen"}],"signature":"tick(timerId)","slotKey":"-1"},"key":"2"}],"methods":[],"events":[]}
```
