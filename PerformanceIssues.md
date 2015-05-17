<p>I've uploaded a special version of my emulator that doesn't throttle the framerate, so that we can accurately gauge speed and performance. Please see <a href='http://goo.gl/648IU'>http://goo.gl/648IU</a></p>

<p>Notice in Chrome 11 the emulator is running Super Mario 3 at <b>96 fps</b></p>

<img src='http://gwt-nes-port.googlecode.com/svn/wiki/ScreenshotChrome11.png' border='2' />



<p>And in Chrome 13 the emulator is running Super Mario 3 at <b>48 fps</b></p>

<img src='http://gwt-nes-port.googlecode.com/svn/wiki/ScreenshotChrome13.png' border='2' />

<p>When I profiled, the following IF / ELSE block has two operations where it writes to arrays. When commented out, I gain back 30 fps:<br>
<br>
<pre><code>function $backgroundBlitzer(this$static) { <br>
  ..... <br>
  for (i = 0; i &lt; 33; ++i) { <br>
    MMC5_pal = mapper.PPU_Latch_RenderScreen(1, nameAddr &amp; 1023); <br>
    MMC5_pal != 0 &amp;&amp; (attribBits = MMC5_pal &amp; 12); <br>
    patternValueLo = $ppuRead_0(this$static, patternAddr); <br>
    patternValueHi = $ppuRead_0(this$static, patternAddr + 8); <br>
    this$static.latchMapper &amp;&amp; mapper.latch(patternAddr); <br>
    patternMask = 128; <br>
    for (int patternMask=0; patternMask &gt; 0; patternMask &gt;&gt;= 1) { <br>
      col = attribBits; <br>
      (patternValueLo &amp; patternMask) != 0 &amp;&amp; (col |= 1); <br>
      (patternValueHi &amp; patternMask) != 0 &amp;&amp; (col |= 2); <br>
      if ((col &amp; 3) != 0) { <br>
        // If I comment out below 2 lines, perf increases 30 fps<br>
        this$static.solidBGPixel[solid] = 1; <br>
        this$static.linePalettes[p] = col; <br>
      } <br>
       else { <br>
        // If I comment out below 2 lines, perf increases 30 fps<br>
        this$static.solidBGPixel[solid] = 0; <br>
        this$static.linePalettes[p] = 0; <br>
      } <br>
      ++solid; <br>
      ++p; <br>
   } <br>
   ..... <br>
} <br>
<br>
</code></pre>