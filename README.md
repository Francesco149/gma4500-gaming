the gma4500 is an old on-board GPU that some old laptops use. this list is an effort to provide
info on expected performance and various performance tweaks that work well on this gpu

all information is released into the public domain

the test machine is a thinkpad x200:

* fullscreen resolution is 1280x800
* cpu: Intel Core 2 P8600 2.4GHz
* librebooted
* no overclocking
* 4 GB ram
* os: linux (parabola with a deblobbed, fsync-enabled kernel)

for wine games:
* wine versions are tkg-patched unless specified
* ESYNC/FSYNC are enabled unless specified
* limits.conf already set up for esync (google how to do it)

some tips that apply to all games:
* run with `vblank_mode=0 game` to make sure there's no fps cap other than the ingame settings
* kill your compositor (I have picom, so I just `killall picom`)
* set up zram to almost double your ram capacity for a small cpu overhead hit

# monitoring tools
## glxosd
I made a patched version to fix compilation errors and remove dependency on the proprietary nvidia
lib. install glxosd-fix-git from aur

works better than mangohud on this old gpu

## mangohud (tool to show fps and stats)
I made a patched mangohud that works on this gpu, it's in arch aur, mangohud-opengl2

many games are buggy with it though, for example xonotic blackscreens and 0ad crashes

# Terraria (GOG version)

    Kernel 5.8.13-gnu-1
    Mesa 20.2.2-2

stable 60fps at 800x600

* set lighting to "trippy" for a massive fps boost
* quality: low, background: off, heat distortion: disabled, storm effects: disabled,
  waves quality: off

# 0ad

    Kernel 5.8.13-gnu-1
    Mesa 20.2.2-2

~30 fps at lowest settings fullscreen

* disable glsl in graphic options for a major fps boost
* ideally play with all graphics settings at lowest

put the following in `~/.config/0ad/config/local.cfg`

    novbo=true

# xonotic

    Kernel 5.8.13-gnu-1
    Mesa 20.2.2-2

80-150fps at 640x480, 50-80fps at full resolution

* use the `xonotic-sdl` executable, it performs slightly better for some reason
* on video disable vbo's and "use glsl to handle color control" but leave OpenGL 2.0 shaders enabled
* on effects set everything to low
* open the console with the tilde/backtick key (left of 1) and type

        r_showsurfaces 3
        r_sky 0
        showfps 1
        saveconfig

# Pocket Mirror (wine)

    Kernel 5.8.13-gnu-1
    Mesa 20.2.2-2
    wine-5.21.r9.g0192a7b3 (Staging)

60fps, resolution is fixed at 640x480

# openarena

    Kernel 5.8.13-gnu-1
    Mesa 20.2.2-2

stable 125fps locked at 640x480

* press the tilde/backtick key to open the console and type

        r_vertexLight 1
        cg_simpleItems 1
        r_drawFPS 1
        com_maxfps 125
        writeconfig autoexec.cfg

# minetest

30-50 fps in fullscreen, 60fps if you resize the window to roughly 800x600, but the game has no
way to fullscreen it scaled at low res so you're stuck playing in a small window

disable everything in graphical options, set leaves to opaque
