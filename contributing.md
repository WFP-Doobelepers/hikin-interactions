# Hikin Contribution Guide

There's several steps involved with making Hikin run your own commands. This guide does not cover how to host a discord bot, but simply issues steps on how to add commands and other material to Hikin for Wangsheng Funeral Parlor Theorycrafting.

- Install Requirements.

    These are one time installations. Feel free to skip this step if requirements are already fulfilled.
    
    1. Install [VS Code](https://code.visualstudio.com/download).
    
    2. Install [Git](https://git-scm.com/download/win).
    
    3. Clone the repository to your local storage using the following command:
    
    ```bash
    git clone https://github.com/WFP-Doobelepers/hikin-interactions
    ```
    4. Open the folder where the repository is cloned in VS Code.
    
      VS Code will automatically determine that this is a cloned repository.

## Creating a new Command:

A new command can be created by adding a folder under the commands section of the bot as well as under the interactions         section for adding interaction(s) for the command. The bot reads .yaml files to create all the commands.
  
### __Folder Structure:__

Various subfolders can be added to these folders to designate elements/properties about the character and overall               file organization.
    
For example, when creating an FAQ for various Genshin Impact Characters, the folder structure may look like this: 
    
<img src="https://user-images.githubusercontent.com/66517217/226588052-c8db5de9-7300-4c77-b4d9-e830851f53a9.png" width = "300">
   
### __Adding a Character Command under Hikin :__

Suppose we need to add the Genshin Impact Character "Hu Tao" to display under one of our pre-existiing commands "FAQ", we first need to create a `character.yaml` file for that character under the appropriate element folder, in this case `"commands/faq/pyro"`.

<img src="https://user-images.githubusercontent.com/66517217/226590378-87b66629-2d38-4880-907e-47add689f8cd.png" width = "300">

Now we need to add an `interaction`, `description` and `name` for the command in the .yaml file format.

<img src="https://user-images.githubusercontent.com/66517217/226590718-24294bfb-4fe6-4b82-8e05-066589f83213.png" width = "300">

The `interaction` field will always point to the `main.yaml` file under the interaction for that character, which we will discuss below.

### __Adding an Interaction for a Character under Hikin:__

An "interaction" is simply a task the bot does when a command is executed. The content under the interaction folder tells Discord Bots what to do when a command is executed. 

Just like the `commands` folder, the `interactions` folder also has subfolders corresponding to elements as well as characters:

<imge src="https://user-images.githubusercontent.com/66517217/226593643-f9fd1287-b98f-4208-ac14-aea2ae1fdce6.png"  width = "300">

To add your own character, add a folder under the appropriate element by that character's name :

<img src = "https://user-images.githubusercontent.com/66517217/226593962-a37662f0-7d28-4b1d-a9ef-4994f51ca83d.png"  width = "200">

This folder path `interactions/faq/hutao/` will contain the `main.yaml` and other `.yaml` files associated with the content of the character. 

For FAQs, a files can be created for topics that can be listed in a dropdown:

<img src="https://user-images.githubusercontent.com/66517217/226594644-bc4d8f30-1ac8-4194-94da-49b89b1f4805.png"  width = "200">

These files are then linked to `main.yaml` using buttons.

### __Adding an Embed__

 Discord.js can read `.yaml` files to create an embed that will be displayed on running a command.
 
 An example embed is :
 
 ```yaml
content: null # can be left null
embed:
  - title: This is a Hu Tao FAQ
    description: >-
      Hu Tao is Amazing! 
    color: 12328992 #image color should be converted from hexadecimal to integer
    fields:
    - name: 'Hu Tao is also called'
      value: >-
        Walnut
    footer:
      text: 'Hu Tao Wrote This~'
    image:
      url: hutao.jpeg
    thumbnail:
      url: hupfp.png
    author:
      name: 'Hu Tao'
      icon_url: hutaotao.png
 ```

### Adding a Dropdown Option

Dropdowns can be added alongside embeds. These dropdowns allow the user to access all the content through a list. In Hikin these buttons should be added to the `element/character/main.yaml` file for a specific character.

_**NOTE:**_ You Need to add `options:` only once per file.

Template :

```yaml
options:
  - label: <Name> # Display Name of Option
    value: path/to/the/file
    description: <Description> #small description to what the option leads to
    emoji: <Full emoji name with ID>
```

Example :

```yaml
options:
  - label: Overview
    value: faq/pyro/hutao/overview #leads to overview.yaml
    description: WFP Resources for Hu Tao FAQ.
    emoji: < ${EMOJIS.PYRO} >
```

### Adding Buttons under Embeds

Buttons can be added under embeds. These buttons allow the user to scroll through multiple pages while being on the same dropdown topic or redirect to. Buttons can hence be useful to display a handful of embeds as multiple "pages", specially when the embeds exceed the discord embed limit for a message (10 embeds).

_**NOTE:**_ You Need to add `buttons:` only once per file.

Buttons used in Hikin are of two types:

- Linked Buttons
- Primary Buttons

  **Adding Linked Buttons**
  
  Linked buttons will allow you to access an external link through a browser. These buttons can be added to                       `character/main.yaml`.
  
  An example of Linked Buttons (WFP Website link)
  
  <img src="https://user-images.githubusercontent.com/66517217/226602873-d8bf909b-12af-4289-8886-a72b195be174.png"  width = "200">
  
  Template for Linked Buttons:
  
  ```yaml
  
  buttons:
  - label: <name>
    url: <link>
    emoji: <emoji appended by ID>
    style: LINK
  ```
  Example :
  
  ```yaml
  
  buttons:
  - label: WFP Website
    url: https://wangshengfp.org/faq/hutao
    emoji: Pyro:925598875853668353
    style: LINK
  ```
  
  **Adding Primary Buttons**
  
  Primary Buttons can be added under an embed to scroll to another page.
  
  Example in Discord:
  
  <img src = "https://user-images.githubusercontent.com/66517217/226603953-5a4f207b-6093-4c82-8e7b-ed297f5114ed.png"  width = "125">

  Template for Primary Buttons:
  
  ```yaml
  buttons:
  - customId: liveInteraction#path/to/the/file
    label: <name>
    style: PRIMARY (Primary - Blue, Secondary - Gren, Danger - Red)
    emoji: "▶️"
  ```
  
  Example :
  
  ```yaml
  buttons:
  - customId: liveInteraction#characters/pyro/hutao/teambuilding2
    label: Next
    style: PRIMARY
    emoji: "▶️"
  ```
  
## Committing changes

In the end, you must commit the changes made to this repository. To do this, open terminal in your current folder (type in CMD in the file explorer path)

then, execute these lines:

```bash
git add .
``` 
(make sure to include the dot)

```bash
git commit -m “<Your message>”
git push origin main
```

## Testing changes

To load the committed changes into Hikin bot, type in `/reloadcommands` in the discord text pain and execute it. Your commands should be uploaded! Happy Theorycrafting <:)

