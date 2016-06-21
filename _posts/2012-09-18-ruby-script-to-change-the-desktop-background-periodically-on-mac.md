---
layout: post
title: 'Script to change the desktop background periodically on Mac'
---

There is this website that puts out geeky t-shirts for sale everyday - <a title="Teefury" href="http://www.teefury.com/" target="_blank">Teefury</a>. I love their t-shirts and have bought a few from them. But here is the deal with it. You get to buy a tee only on the day it is put out, for $10. After 24 hours it is gone. So, if you forgot to check the website everyday you probably missed a tee you thought would be cool to have.

What could I do so that I don't miss on any of the cool tees again? I figured if i could write a script that would set my computers background daily to that days teefury tee, then nothing like it. So this is how i wrote a crude script that helps achieve it.

Googling around pointed me to this command -
<pre>defaults write com.apple.desktop Background '{default = {ImageFilePath = "~/Downloads/Teefury-Wallpapers/wallpaper.jpg"; };}'</pre>
Once you have this, all the script needed was :
1. A HTML parser to parse the sites homepage to fetch the days teefury image.
2. A way to schedule your script to execute daily automatically.

And you get <a title="this" href="https://github.com/warunsl/Teefury-Wallpaper/blob/master/teefury.rb" target="_blank">this</a>. Suggestions and critiques <a title="welcome" href="https://twitter.com/warunsl" target="_blank">welcome</a>.
