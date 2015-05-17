# Introduction #

This is a port of an existing open-source Java emulator, hacked to compile with GWT and run within the browser using HTML5 technology. Our inspiration was the [@GoogleIO](http://twitter.com/#!/GoogleIO) presentation of the [quake2-gwt-port](http://code.google.com/p/quake2-gwt-port/) project, a pure HTML5 port of the popular Quake2 video game.

We really wanted to take advantage of the power of Chrome and HTML5, so you will find some pretty cool features, including:
  * Use of HTML5 File API to upload games
  * Use of Local Storage / WebDB to store games
  * Ability to play games offline. You never need an Internet connection
  * Use of the Canvas to render games, no flash plugin!

There is no profit in this. We don't sell the game. We don't display ads. It's just a fun project to showcase the power of HTML5, the speed of Google Chrome, and to help the world to transition to ChromeOS without missing some of their favorite desktop apps (in this case, NES emulators).

# Compatibility #

This emulator is compatible with the following mapper's:

  * Mapper 0 - Super Mario Bros, Excite Bike, Kung Fu ...
  * Mapper 1 - Legend of Zelda, Metroid, Rad Racer, Mega Man 2 ...
  * Mapper 2 - Castlevania, Mega Man, Contra, Duck Tales ...
  * Mapper 3 - Spy Hunter, Paperboy, Goonies ...
  * Mapper 4 - Super Mario Bros 2 and 3, Mega Man 3, 4, 5, and 6
  * Mapper 5 - Castlevania 3 ...
  * Mapper 7 - Battletoads, Cobra Triangle ...
  * Mapper 9 - Mike Tyson's Punchout

Mappers 0-9 represent the vast majority of popular NES games. We do have the source code for the additional mappers, but have not yet integrated them into our project.

# Performance #

The emulator performs very well in the later version of Chrome, on modern laptops, and is able to achieve frame rates that **exceed 120 FPS** for games like Super Mario 3.

Unfortunately, on Netbooks (including the CR-48), and in Firefox 4, we are only able to achieve frame rates of approx 20-30 FPS, which pretty much renders the emulator worthless. Luckily for us, Moore's law says this probably won't be an issue in a year or two.