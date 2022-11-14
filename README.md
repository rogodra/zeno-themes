# Zeno Themes - by rogodra

<br><br>
# If you STILL DON'T have the "themes" folder

You need to configure your **configuration.yaml** file, adding the code below for your Home Assistant to search for themes in the **themes** folder:

```
frontend:
  themes: !include_dir_merge_named themes
```

**ATTENTION! It is necessary to restart after this configuration!**

# Installation via HACS (Home Assistant Community Store)
(If you are not HACS) [Learn how to install](https://hacs.xyz/docs/installation/manual)

* Go to the HACS Community Store
* Click on the **"Frontend"** option
* Click on the **(+)** button
* Search for **"Zeno Themes"**
* Click **"Install"**
* Restart your Home Assistant


# Manual installation

Then download the **zeno-themes.yaml** [**clicking here**](https://bit.ly/) and copy the file to your **themes** folder.<br>
If your **themes** folder does not yet exist, you must create it within the **config** folder


## Download backgrounds and icons (only required for manual installation)
10 of the 40 themes have backgrounds and all themes use animated icons for the weather forecast card. These files need to be downloaded and copied to your Home Assistant server.

1. Download the backgrounds and icons [**clicking here.**](https://bit.ly/)
2. Extract the file **.Zip**
3. Copy the folder **zeno-themes** into the folder **config/www/**. The final path to the file folder should be **config/www/zeno-themes/**

*ATTENTION! If your **www** folder does not yet exist, create it within the **config** folder. *

Now **restart your Home Assistant** and the themes will be available for use.
<br><br>


# Creating an automatic theme selector for the interface (optional)
We will create a theme selector to be implemented in your user interface. It is a practical way to change the theme instantly on all devices connected to your Home Assistant. See how it works in the gif below:


![](https://raw.githubusercontent.com/rogodra/zeno-themes/master/docs/seletor.gif)

## 1st Step - Creating the input_select
The input_select will be used to create the selection list with the themes that I created. <br>
Insert this code into your file **configuration.yaml**<br>
If you've never used input select, [learn more by clicking here.](https://www.home-assistant.io/integrations/input_select)<br><br>

```
input_select:

  themes:
    name: 'Themes'
    icon: mdi:format-paint
    options:
      - Zeno Dark Rose
      - Zeno Dark Purple
      - Zeno Dark Blue 
      - Zeno Dark Aqua
      - Zeno Dark Green
      - Zeno Dark Yellow
      - Zeno Dark Orange
      - Zeno Dark Coral
      - Zeno Dark Pink
      - Zeno Dark Gray
      - Zeno Light Rose
      - Zeno Light Purple
      - Zeno Light Blue 
      - Zeno Light Aqua
      - Zeno Light Green
      - Zeno Light Yellow
      - Zeno Light Orange
      - Zeno Light Coral
      - Zeno Light Pink
      - Zeno Light Gray
      - Zeno Black Rose Glass
      - Zeno Black Purple Glass
      - Zeno Black Blue Glass 
      - Zeno Black Aqua Glass
      - Zeno Black Green Glass
      - Zeno Black Yellow Glass
      - Zeno Black Orange Glass
      - Zeno Black Coral Glass
      - Zeno Black Pink Glass
      - Zeno Black Gray Glass      
      - default
```
Restart your Home Assistant so that the input_select is created.


Result:
* input_select.themes



## 2nd Step - Theme selector automation

### Attention! This automation is available in two methods. Choose only one method.

### Method 1) Native Automation of Home Assistant with YAML

Copy the code below and paste it into your file **automations.yaml**

```
- alias: "set Themes"
  initial_state: true
  trigger:
    platform: state
    entity_id: input_select.themes
  action:
  - service: frontend.set_theme
    data_template:
      name: >
        {{ trigger.to_state.state }}
```


### Method 2) Automation with Node-RED

**WARNING!** If you've never used Node-RED, [learn more by clicking here.](https://github.com/hassio-addons/addon-node-red)


We will create a flow in Node-RED to define the theme automatically every time you choose a theme in your interface. It's very simple! Just download the .json file or copy the code and paste it into the Node-RED import window.

![](https://raw.githubusercontent.com/rogodra/zeno-themes/master/docs/nodered.gif)

[Click here to copy or download the code for Node-RED flows](https://bit.ly/3gLMtrs)

After importing the flow to your Node-RED, click **Deploy**<br><br>

## 3rd Step - Implementing the selector in your interface

Now just insert the selector code in your interface.
* If you use the interface in YAML Mode, copy the code and insert it into your **ui-lovelace.yaml**
* If you use the interface in automatic mode, go to the editing mode of your interface, choose the "manual" option at the end, then copy and paste the code below.

``` 
  type: entities
  show_header_toggle: false
  entities:
    - entity: input_select.themes

``` 

## 4th Step - Configuring the "Backend-selected" theme

Change the theme in the user's profile to "Backend-selected". This way, all connected devices with the theme "Backend-selected" will have their themes changed synchronously with the theme selector you just created.
