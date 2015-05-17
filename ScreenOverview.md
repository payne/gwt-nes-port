# Game Library Screen #

The game library screen is the application's home screen. Games are displayed in the main content area, represented by their name and box cover.

Games are tagged by Genre, and there are links on the left side of the screen that let you filter your game library by Genre. You may also search for games by name, using the search box.

<img src='http://gwt-nes-port.googlecode.com/svn/wiki/GameLibraryScreen.png' width='700px' />


# Import Game Screen #

You can import games directly from your filesystem, thanks to the HTML5 File API. You can either use the File dialog box, or drag your files directly on to the page. NOTE: dragging multiple files at once is now supported.

<img src='http://gwt-nes-port.googlecode.com/svn/wiki/GameImportScreen.png' width='700px' />

IMPORTANT: All files must have a `.NES` extension. We do not have the functionality to import zipped games.

Once you upload a game, we attempt to match the file name with a pre-defined list of games. Nothing fancy here. No web service call. Just a hard coded list of regular expressions that try to identify the game's title, genre and image.

You can see your games stored in Chrome's local database:

<img src='http://gwt-nes-port.googlecode.com/svn/wiki/GameStorage.png' width='700px' />

# Game Popup #

When you click a Game in your library, the cartridge is loaded and the Game starts. Use your keyboard to control the game: A (X), B (Z), Select (Ctrl), Start (Enter) and the Arrow keys for direction. The zoom icons can be used to increase / decrease the screen size, and the shutdown icon will stop the game and return to the home screen.

IMPORTANT: make sure the page has focus, otherwise your keyboard events won't register

<img src='http://gwt-nes-port.googlecode.com/svn/wiki/screenshot3.png' width='700px' />

# Settings Screen #

The settings screen doesn't do too much at the moment. It displays the current controller keyboard mappings, however, it does not provide the ability to modify the keyboard mappings. We hope to fix this in a future release.

<img src='http://gwt-nes-port.googlecode.com/svn/wiki/GameSettingsScreen.png' width='700px' />

# Design Goals #

Our goal was to design a UI that matched the Google Chrome look and feel. For example:
  * The color palette matches the Chrome New Tab screen
  * The page links (upload game, settings) match the bookmarks on the New Tab screen
  * The game icons match the App icons on the New Tab screen
  * The headings on the Settings and Import Game pages match the headings on the chrome://settings page

If ChromeOS ever releases more comprehensive look and feel guidelines we'll attempt to conform. We want this to feel like it was built for ChromeOS ... because it was!