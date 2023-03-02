# Installing Anaconda

[Python][python] is a popular language for scientific computing, and great for
general-purpose programming as well. Installing all of the scientific packages we use in the lesson
individually can be a bit cumbersome, and therefore recommend the all-in-one
installer [Anaconda][anaconda].

## Windows

1. Open <https://www.anaconda.com/products/individual> in your web browser.
2. Download the Anaconda Python 3 installer for Windows.
3. Double-click the executable and install Python 3 using the recommended settings.
   Make sure that **Register Anaconda as my default Python 3.x** option is checked --
   it should be in the latest version of Anaconda.
4. Verify the installation:
   click Start, search and select `Anaconda Prompt` from the menu.
   A window should pop up where you can now type commands
   such as checking your Conda installation with:

```bash
conda --help
```

<iframe width="560" height="315" type="text/html" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" src="https://www.youtube-nocookie.com/embed/xxQ0mzZ8UvA?modestbranding=1&playsinline=1&iv_load_policy=3&rel=0" class="yt-frame" allowfullscreen></iframe>

## MacOS

1. Visit <https://www.anaconda.com/products/individual> in your web browser.
2. Download the Anaconda Python 3 installer for macOS.
   These instructions assume that you use the graphical installer `.pkg` file.
3. Follow the Anaconda Python 3 installation instructions.
   Make sure that the install location is set to "Install only for me"
   so Anaconda will install its files locally, relative to your home directory.
   Installing the software for all users tends to create problems in the long run
   and should be avoided.
4. Verify the installation:
   click the Launchpad icon in the Dock, type Terminal in the search field, then click Terminal.
   A window should pop up where you can now type commands
   such as checking your conda installation with:

```bash
conda --help
```

<iframe width="560" height="315" type="text/html" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" src="https://www.youtube-nocookie.com/embed/TcSAln46u9U?modestbranding=1&playsinline=1&iv_load_policy=3&rel=0" class="yt-frame" allowfullscreen></iframe>

## Linux

1. Open <https://www.anaconda.com/products/individual> in your web browser.
2. Download the Anaconda Python 3 installer for Linux.
3. Install Anaconda using all of the defaults for installation.
   - Open a terminal window.
   - Navigate to the folder where you downloaded the installer.
   - Type `bash Anaconda3-` and press <kbd>Tab</kbd>.
     The name of the file you just downloaded should appear.
   - Press <kbd>Return</kbd>
   - Follow the text-only prompts.  When the license agreement appears (a colon
     will be present at the bottom of the screen) press <kbd>Spacebar</kbd> until you see the
     bottom of the text. Type `yes` and press <kbd>Return</kbd> to approve the license. Press
     <kbd>Return</kbd> again to approve the default location for the files. Type `yes` and
     press <kbd>Return</kbd> to prepend Anaconda to your `PATH` (this makes the Anaconda
     distribution your user's default Python).
4. Verify the installation:
   this depends a bit on your Linux distribution, but often you will have an Applications listing
   in which you can select a Terminal icon you can click. A window should pop up where you can now
   type commands such as checking your conda installation with 

```bash
conda --help
```

[anaconda]: https://www.anaconda.com/
[jupyter]: https://jupyter.org/
[python]: https://www.python.org/
