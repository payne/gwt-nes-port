# Instructions #

The gwt-nes-port includes both the 8-bit-hits chrome application and a stand-alone emulator that you can directly embed in your own project.

To use the emulator, first create an instance of the `NES` class, which is the guts of the emulator. Also, create an instance of the `TVController` (bad name, I know). The `TVController` class extends GWT's `Widget` and is responsible for `Canvas` rendering and `MouseEvents`, and can be added to the `RootPanel`

```
NES nes = new NES();
TVController gui = new TVController(nes);
```

Next initialize the Emulator:
```
nes.init(gui);  
```

Add the `TVController` to the `RootPanel`:
```
RootPanel.get().add(gui);
```

And finally, when ready, load the Game, which should be in the form of a byte array:
```
byte[] cartridge = ...
nes.cartLoad(new ByteArrayInputStream(cartridge));
```

# Emulating JRE Classes #

If you try to run this code as-is, you will run into some problems. This is because GWT does not currently emulate any `java.io` classes, such as `ByteArrayInputStream`.

We can emulate the classes ourse. In your gwt.xml file, instruct GWT that you will be emulating classes, with the following declaration:
```
<super-source path='jre'/>
```

Then add a folder called "jre" to your project, in the same directory as your gwt.xml file:
```
/com/myproject/MyProject.gwt.xml
/com/myproject/client/
/com/myproject/jre/
```

Then you can add your emulated classes to the jre folder. For `java.io` and `ByteArrayInputStream` it should look something like this:
```
/com/myproject/jre/java/io/InputStream.java
/com/myproject/jre/java/io/ByteArrayInputStream.java
/com/myproject/jre/java/io/IOException.java
```

When GWT compiles, and cannot find the emulated class in the GWT distribution, it will check your local class emulation directory. Check out this project's source code if you are having difficulty.