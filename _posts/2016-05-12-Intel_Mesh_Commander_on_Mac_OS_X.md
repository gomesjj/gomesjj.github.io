---
title: Intel Mesh Commander on Mac OS X
header:
  teaser: "meshcommander.png"
category: [Apple] 
tags: [Mac, OS X, NW.js, Homelab, Virtualisation, NUC]
---

Intel Active Management Technology is one of the hardware technologies (perhaps the most recognised and representative) that is part of Intel's [vPro](http://www.intel.co.uk/content/www/uk/en/architecture-and-technology/vpro/vpro-technology-general.html) offerings. AMT offers the benefits of out-of-band management similar to IPMI, but for personal computers as opposed to servers.

*[IPMI]: Intelligent Platform Management Interface

When I was selecting the NUC model(s) to use for my ESXi home lab, the fact that both the [DC53427HYEA](http://www.intel.co.uk/content/www/uk/en/nuc/nuc-kit-dc53427hye-board-d53427rke.html) and the [NUC5i5RYH](http://www.intel.co.uk/content/www/uk/en/nuc/nuc-kit-nuc5i5ryh.html) sported processors with vPro and AMT support helped me sway towards them. The NUCs were replacing kit that had full IPMI functionality, and I knew how much I would miss the convenience of managing the new "servers" remotely. 

There was a little fly in the ointment though. As I researched the technology it became clear that all the management tools were Windows only. Even Linux support was almost non-existent except for some example code distributed with the AMT SDK. Bummer, I thought to myself, another "Macs need not apply" zone.

I do run a Windows 7 VM on my laptop solely because of Visio (another bummer), so I resined to the fact that the VM would just have to spin a few more times a week. That is, until I came across [Mesh Commander](http://www.meshcommander.com/meshcommander). Mesh Commander is open source software developed by Intel's Ylian Saint-Hilaire, which is distributed as a WIN64 binary or as a website served from IIS (Yuck!). Since the IIS version included the source code, I decided to download it and see if I could coerce the code to run on Apache or something else. To my surprise, in the bowels of the source code, I found an NW.js folder. That was more like it!

*[IIS]: Internet Information Services

I dabble from time to time with some coding and scripting, particularly when I want to have some piece of software running on Mac OS X; but, I had never played with NW.js (née node-webkit). If you are not familiar with NW.js, you can see what it is all about [here](http://nwjs.io).

To start with, I downloaded version 0.1.3 of Mesh Commander (it's now at 0.2.0) and version 0.12.3 of NW.js (stable is 0.14.5 now). I must confess I had much more problems with the code than I expected, but I think it was down to NW.js. Since then I have tested with later versions and the total amount of changes to the source code is now insignificant, amounting to just a couple of Mac OS X specific GUI items.

So, lets move on to the recipe.

### The Ingredients

1\. Apple Developer ID

You will need a valid Developer ID and signing certificate, otherwise the resulting application will not even run. The Mac Developer Program costs GBP 79 / USD 99 per year for an individual.

[Apple Developer Program](https://developer.apple.com/programs/)

{: .notice--info}
Have you had enough already and don't want to bake anymore? You can download one that I prepared earlier, fully signed, [here](https://bintray.com/gomesjj/APPS/download_file?file_path=OSX%2FMeshCommander.dmg.zip).

2\. Xcode

If you haven't installed Xcode yet, get it from the App Store, or download from [ Developer](https://developer.apple.com/xcode/download/). 

Time for a cuppa of whatever rocks your boat, as it will take some time...

3\. Install ```node```:

The easiest way is by installing Homebrew first

```sh
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
Now, you could just install ```node``` and ```npm``` straight away, but I recommend you follow the instructions in this [post](https://johnpapa.net/how-to-use-npm-global-without-sudo-on-osx/) by John Papa. The instructions show how to use ```npm global``` without the need for ```sudo```.

***or***

If you don't mind running code compiled by someone else, just install the ```node``` binary, which also includes ```npm```. Download it from [here](https://nodejs.org/en/download/).

4\. Install ```nw-builder```:

```sh
npm install -g nw-builder
```
I have used both ```nw-builder``` and ```nwjs-macappstore-builder```. Whilst both of them work well, I prefer ```nw-builder``` as it offers more control.

If you would rather decide for yourself, have a look at [nw-builder](https://github.com/nwjs/nw-builder) and [nwjs-macappstore-builder](https://www.npmjs.com/package/nwjs-macappstore-builder).

5\. Grab the modified source files and other requisites from my GitHub [repository](https://github.com/gomesjj/MeshCommander)

### Lets bake it

1\. Create a directory to store the files and the built application.

```sh
mkdir -p ~/devel
``` 

If you downloaded the contents of my repository, just copy them over to the above created folder. You can also clone the contents directly with ``git``

```sh
cd ~/devel
git clone https://github.com/gomesjj/MeshCommander.git
```
You should end-up with something like this

```sh
ls
MeshCommander/

ls -lR MeshCommander
total 16
-rw-r--r--  1 gj1606  staff    90B 4 May 14:00 README.md
-rwxr-xr-x  1 gj1606  staff   1.8K 4 May 14:00 mkapp*
drwxr-xr-x  5 gj1606  staff   170B 4 May 14:00 files/
drwxr-xr-x  7 gj1606  staff   238B 4 May 14:00 source/

MeshCommander/files:
total 88
-rw-r--r--  1 gj1606  staff   2.6K 4 May 14:00 Info.plist
-rw-r--r--  1 gj1606  staff   600B 4 May 14:00 InfoPlist.strings
-rw-r--r--  1 gj1606  staff    36K 4 May 14:00 meshcommander.icns

MeshCommander/source:
total 3504
-rw-r--r--  1 gj1606  staff   1.7M 4 May 14:00 Commander.htm
-rwxr-xr-x  1 gj1606  staff   3.6K 4 May 14:00 favicon.ico*
-rwxr-xr-x  1 gj1606  staff   3.1K 4 May 14:00 favicon.png*
-rw-r--r--  1 gj1606  staff   593B 4 May 14:00 package.json
-rw-r--r--  1 gj1606  staff    18K 4 May 14:00 scriptblocks.txt
```
2\. Build the application

```sh
cd MeshCommander
. ./mkapp
```
If the build is successful you should see output similar to this:

```
node:61321) fs: re-evaluating native module sources is not supported. If you are using the graceful-fs module, please update it to a more recent version.
  downloading [====================] 100% 0.0s

all done!

Copying "InfoPlist.strings" to "en.lproj" directory

Signing Application

./build/MeshCommander/osx64/MeshCommander.app/Contents/Versions/51.0.2704.47/nwjs Framework.framework/Helpers/crashpad_handler: signed Mach-O thin (x86_64) [crashpad_handler]
./build/MeshCommander/osx64/MeshCommander.app/Contents/Versions/51.0.2704.47/nwjs Framework.framework/Resources/APP_mode_loader.APP/Contents/MacOS/APP_mode_loader: signed app bundle with Mach-O thin (x86_64) [io.nwjs.nw.app.@APP_MODE_SHORTCUT_ID@]
./build/MeshCommander/osx64/MeshCommander.app/Contents/Versions/51.0.2704.47/nwjs Helper.APP/Contents/MacOS/nwjs Helper: signed app bundle with Mach-O thin (x86_64) [io.nwjs.nw.helper]
./build/MeshCommander/osx64/MeshCommander.app: signed app bundle with Mach-O thin (x86_64) [com.intel.MeshCommander]

Verifying signature

Executable=/Users/gj1606/devel/MeshCommander/build/clone/MeshCommander/build/MeshCommander/osx64/MeshCommander.app/Contents/MacOS/nwjs
Identifier=com.intel.MeshCommander
Format=app bundle with Mach-O thin (x86_64)
CodeDirectory v=20200 size=311 flags=0x0(none) hashes=3+4 location=embedded
Hash type=sha256 size=32
CandidateCDHash sha1=e3afaf1ada749b9e2617ff53c25761ec9b5125a7
CandidateCDHash sha256=b25da72bd96ab5ffbbeda9e0094846c53ea23757
Hash choices=sha1,sha256
CDHash=b25da72bd96ab5ffbbeda9e0094846c53ea23757
Signature size=8908
Authority=Developer ID Application: Jose Gomes (3JU95247N3)
Authority=Developer ID Certification Authority
Authority=Apple Root CA
Timestamp=13 May 2016, 15:22:34
Info.plist entries=28
TeamIdentifier=3JU95247N3
Sealed Resources version=2 rules=12 files=86
Internal requirements count=1 size=184


Veriyfing Gatekeeper acceptance...

./build/MeshCommander/osx64/MeshCommander.app: accepted
source=Developer ID
override=security disabled
```

**Note:** On first run, NW.js is downloaded and cached locally for subsequent builds:

```sh
<SNIP>
  downloading [====================] 100% 0.0s
</SNIP>

ls cache/
0.15.0-rc2/
```
The packaged application will be under the **build** directory:

```sh
ls ./build/MeshCommander/osx64/
MeshCommander.app
```

### Look what's come out of the oven


![Start](/images/mesh/mesh.png)

![About](/images/mesh/about.png)

![Status](/images/mesh/status.png)

![Hardware](/images/mesh/hw.png)

![Remote](/images/mesh/rdesk.png)

### Can I eat it?

Yes, you can. Download the application:

[MeshCommander.app](https://bintray.com/gomesjj/APPS/download_file?file_path=OSX%2FMeshCommander.dmg.zip)
