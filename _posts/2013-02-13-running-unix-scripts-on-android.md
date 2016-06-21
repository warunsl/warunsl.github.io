---
layout: post
title: 'Running unix scripts on Android'
---

It's a known problem on Android ecosystem that developers abuse the app development good practices by choosing to store their app data randomly on the internal storage (or external storage). They should instead be putting their data in /Android/data. Yet another abuse is by apps which store images and other media on the internal storage and don't include a .nomedia file. This ends up polluting your Gallery app with images and media you don't want to see in there.

Whatsapp is an app I use daily, has millions of users worldwide and pretty popular chat client in India. This app abuses both the good practices I noted above. While we can't change the first, there is certainly something we can do about the second issue. Create a file in the directory Whatsapp stores the images (It's usually /storage/emulated/0/Whatsapp/Media/Whatsapp Images), name it .nomedia and you should be done. Turns out, this is not enough. The .nomedia file's functionality is overridden once Whatsapp stores new images in this folder. So, you need to be able to program your phone to create the .nomedia file periodically or create the .nomedia file every time Whatsapp writes a new image to it's image directory.

There is an app on Android called <a href="https://play.google.com/store/apps/details?id=os.tools.scriptmanager&amp;hl=en">Script Manager</a> that let's you run Unix scripts in your phone. So, you could install that app and create a script which creates a .nomedia file in the Whatsapp's image directory. The app also lets you schedule your script to run at regular intervals. So, the following script scheduled to run once a day should take care of the issue noted above.


     #!/system/bin/sh
     touch /storage/emulated/0/Whatsapp/Media/Whatsapp\ Images/.nomedia


It would have been even better if we could run this script only when Whatsapp stored a new image in it's images folder. I could not find a way to enable filesystem listeners to accomplish this. Do let me <a href="https://twitter.com/intent/tweet?screen_name=warunsl">know</a> if there is way to do this.
