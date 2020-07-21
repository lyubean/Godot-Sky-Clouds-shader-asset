#####

Sky with Clouds asset by Leo Gallatin
My code is MIT, reused code licenses are listed below

Godot Clouds asset by Danil S, based on https://www.shadertoy.com/view/XtBXDw ( Godot code MIT / shader code CC BY-NC-SA 3.0)
Godot Sky asset by Bastiaan Olij, based on https://github.com/wwwtyro/glsl-atmosphere (Shader code Unlicensed / Godot code MIT license / Panorama of Night Sky Copyright of Serge Brunier)

Version 1.0
Working in Godot 3.2.2 July 20th, 2020

---

Hello! This is an asset I thought I would publish since I have seen other people trying to do this exact same thing. 
I would not call this asset "complete" at the moment, as I have quite a few things I want to add, but it is functional enough that I thought I would publish it for now.

This asset is a combination of two assets made by two others that were both originally pure GLSL scripts by two other people. I edited the two shaders into one shader and the Godot scripts into less godot scripts.

This asset contains a shader that renders a Panoramic Sky for use as a skybox. It also contains scripts and scenes for that exact purpose, and a couple textures that are necessary for the shader to work as intended.
For now, the shader cuts off around the horizon line, so you will want to either add your own shader content under the horizon line or hide the horizon line with geometry.

I plan to add more features like the clouds and sunlight color reflecting the sky color during sunsets and sunrises, the clouds changing gradually based on a "weather" controller, the sun going across the sky at an angle and being able to change that angle based on how long a day should last, and then the length of a day and kinds of weather be determined by the day of the year. Probably also a custom night sky that is not an image so it can be animated. Lots of things to look forward to.

---

How to setup:

Add the folder in this package "addons/Sky" to your project folder. You should then be able to instance the "Skycontrol.tscn" scene into any scene you have.

Make sure that noise.png is set to Repeat: Enabled in the Import tab. If it isn't, change it and reimport.

On your default/active camera, either set the environment to the environment included, "sky_environment.tres", or set your own environment to have a Sky Background using a PanoramicSky.

Hopefully, if all went well, you should be able to compile and see a beautiful sunrise with some giant fluffy clouds!

---

Alright, I will explain briefly how this works, the basic structure is pretty easy:

If you load up the scene "Skycontrol", we have a base node named Skycontrol that has the script "sky_control" attached. This node would be the controller for the sky and clouds, it is responsible for updating the skybox and sun.

Skycontrol has two children, Skybox.tscn and a directional light called Sun.

Skybox.tscn is a simple scene with a viewport root node with the script "skybox_code" and a Sprite child with a texture, which is where the shader "sky_clouds" draws to.

-Node Skycontrol script "sky_control"
   -Viewport Skybox script "skybox_code"
      -Sprite Skytexture shader "sky_clouds"
   -DirectionalLight Sun

Not too many parts.

The script "sky_control" handles the time changes, in it you can set how long you would like a day to last and how often to update sun and environment lighting. This script is like the Skybox's boss, it handles the big picture while the Skybox talks to the shader.
One note, be careful with the environment lighting, it is pretty intensive to update so don't make it update every frame unless you're sure you can handle it.

The script "skybox_code" is supposed to be the direct interface between the shader and scripts. If you want to tell the shader something in the sky_control script you should grab the shader through the skybox_code script.

Feel free to change this asset to your liking. Happy skies to you!