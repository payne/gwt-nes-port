# Overview #

The [HTML5 File API](http://www.html5rocks.com/tutorials/file/dndfiles/) allows the user to upload a File, and allows the browser to process that file (previously server side code was necessary).

GWT does not currently support the File API, so I've added my own support by creating my own implementation via JSNI.

We use the File API so that the user can open and play Games (.net files) located on their hard drive. Our implementation of the File API might be useful to other developers, so I wanted to include a brief overview of how it works. Unit GWT supports the API, feel free to copy and paste from our project.


# Instructions #

To use the File API, first add a `FileUpload` widget to the page:
```
final FileUpload fileUpload = new FileUpload();
```

Then create `ProgressCallback`, which the `FileReader` will use to notify us once it has completed reading the file. In the below snippet, you will notice that I convert the file contents to a `byte[]`, since it is binary data:
```
final ProgressCallback binaryReaderCallback = new ProgressCallback() {

   @Override
   public void onLoad(ProgressEvent e) {
      byte[] bytes = new byte[e.getTotal()];
                                
      //convert the results to a byte array
      String result = e.getResult();
      for(int i=0;i<bytes.length;i++) {
         bytes[i] = (byte) result.charAt(i);
      }
      //now do something with the bytes ... like load the NES cartridge
   };
```

<font color='#555'><i>NOTE: we cannot use <code>e.getBytes()</code> for some reason. It has something to do with the with GWT's emulation of the <code>String</code> class, and limited encoding support. So instead we have to iterate through each character in the <code>String</code> and construct the <code>byte[]</code> ourselves.</i></font>


Now we need to add a `ChangeHandler` to the `FileUpload` widget, so we know when the user has selected a File. When triggered, we will attempt to read the file:

```
fileUpload.addChangeHandler(new ChangeHandler(){

    @Override
    public void onChange(ChangeEvent event) {
                                
        FileList fileList  = FileList.fromEvent(event.getNativeEvent());
        FileReader reader = FileReader.create();
        File file = fileList.get(0);
                                
        reader.readAsBinaryString(file, binaryReaderCallback);
    }
});
```

As you can see, the reader is given the `binaryReaderCallback` to alert us once the File has been processed.

It is also important to note there are other read methods available, such as `readAsText` and `readAsDataURL`. We demonstrated `readAsBinaryString` since `.nes` files are encoded.