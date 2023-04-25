# Rocket League Assistant
BakkesMod Plugin to integrate Rocket League events with Home Assistant

## Discord: [Rocket League Assistant](https://discord.gg/8bNkhCmQXe)

![RLHAbanner](https://user-images.githubusercontent.com/23534272/175837042-8db1aea4-214a-4e69-92ab-2c4c705ffeda.png)

## ⭐Special thanks to those in the Discord and notably [Branky](https://github.com/ItsBranK) and [JerryTheBee](https://github.com/ubelhj)⭐
And some other person named Josh

# Home Assistant Configuration
The plugin utilizes Home Assistant's built in Webhook automation trigger with JSON-based conditions.

## HA Scenes Configuration(Not Required):

1. Create a new scene corresponding to the scenario (Home Team, Away Team, Demos, etc)
2. Give it a name (and icon/area if you'd like)
3. Add entities/devices to the scene and adjust the colors accordingly
4. Save the scene
5. Create a new, or duplicate the scene.
6. Add entities/devices to the scene and adjust the colors accordingly.
7. Save the scene
8. Repeat

[**More on scene creation here**](https://www.home-assistant.io/integrations/scene/)

## HA Webhooks Configuration:

### Option 1 - Generate the base automation using the in-game plugin settings window

1. **Generate a _Long-Lived Access Token_ in Home Assistant**:

   a. Click your username in the bottom left of the Home Assistant web interface
   
   b. Scroll to the bottom under "Long-Lived Access Tokens" and click "Create Token"
   
   c. Give the token a name and press "Ok"
   
   d. Copy the token string. ***It is best to click into the text box and press CTRL-A to select all, and then CTRL-C to copy the selected text***
	
	![HATokenStep1](https://user-images.githubusercontent.com/23534272/234130854-5aafac64-c6b8-47bc-ab5d-90625b864032.png)
    
	![HATokenStep2](https://user-images.githubusercontent.com/23534272/234130913-ce4de667-c4f3-452b-8b1e-2f70fc499f34.png)
	
   You will now have a token similar to this:
   ```eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiI5NTgxMmNlMWIyYmI0OTRhYTIzN2U0NjNiOTIwMmU5MSIsImlhdCI6MTY4MjM2NzE2OSwiZXhwIjoxOTk3NzI3MTY5fQ.9gdUfsDoYXyTPtqi4vIZ0vuRPFZ-fUrSum_4BxEGzcw```
   ***You may want to temporarily paste the code into Notepad or the URL bar***

2. **Use the Template Generator in the plugin's setting window**:


   a. Press F2 in-game `Plugins` tab -> `RocketLeagueAssistant`
   
   b. Expand `Automation Template Generator`
   
   c. Populate your Home Assistant URL and Token generated in step 1
   
   d. Click `Generate Automation Base Template`. Your *Home Assistant Web Hook Global URL* field will be automatically populated with the appropiate URL for Home Assistant. 
    
   ***The token will be automatically erased from the plugin and config file for security reasons. It is suggested to also delete the token from Home Assistant after, so your token can not be used.***

   The plugin configuration is done.
    
   ![RLAGenerateAutomation](https://user-images.githubusercontent.com/23534272/234132236-41fd50aa-6467-49c1-b320-dde76c58b682.png)


 You should now have an automation called ***RocketLeague - BakkesGenerated*** in Home Assistant

3. **Populate each condition with the action corresponding with its condition**:

   ![HAEditConditions](https://user-images.githubusercontent.com/23534272/234131005-bc842736-7ef7-4704-ac5e-f133c3adb462.png)


4. **The color values from the JSON request can be used as the colors for your automations**:
	
	a. Select **Call a service** as your action then edit in YAML.
	
	This will set the color of your lights to the values of your team's primary color. Populate "LIGHTNAMEHERE" with the corresponding entity ID:

```
service: light.turn_on
data:
  rgb_color:
    - "{{ trigger.json.teamColor[0].r |int }}"
    - "{{ trigger.json.teamColor[0].g |int }}"
    - "{{ trigger.json.teamColor[0].B |int }}"
target:
  entity_id: light.LIGHTNAMEHERE
enabled: true
```

![HATeamColorEx](https://user-images.githubusercontent.com/23534272/234131035-115831c2-e365-44be-be14-7884b1da742b.png)

	
	
[**More on automations here**](https://www.home-assistant.io/docs/automation/)	

### Option 2 - Create a new automation using the [**RocketLeague-BakkesBase.yaml**](RocketLeague-BakkesBase.yaml) file.

1. Create a new automation
2. Select **Edit in YAML**
3. Paste the contents of [RocketLeague-BakkesBase.yaml](RocketLeague-BakkesBase.yaml)
4. Edit the actions respectively as shown in Option 1

### Notes

If you manually reload the plugin (through the F6 BakkesMod Console) while in the game, the URL will have to be reentered.

## To Do

* More JSON information
* Probably code clean up and Nullchecks
