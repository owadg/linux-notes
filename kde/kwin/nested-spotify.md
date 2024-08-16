# Goal

I have no idea if it was a bug, but at some point, when I would run `spotify-launcher` and click fullscreen, it wouldn't fullscreen.

I think this was a bug with the `kwin` windowing system, and it was eventually fixed. However, I actually liked this. If you don't know, the fullscreen option in the bottom right hand corner gives a more minimal interface also with custom art based on the artist. It's a nice interface, but I do not want to have it use up the whole screen. It looks better smaller anyways.

So I am trying to make it not use up the full screen.

# Process

At first I tried screwing around with `kwin`'s window rules. They seem to have options to force certain layers and force window size, but I couldn't get these to work. After a little bit of googling, I found that some people have achieved this with a nested compositor. Luckily, `kwin` supports nested compositing.

As `kwin` is relatively robust, it can run programs that use both X and Wayland as X is still a defactor standard and that's what is was built for (I think). Using `xprop` I found that `Spotify for Linux` uses X. So after consulting KDE's documentation on `kwin` [here](https://community.kde.org/KWin/Wayland#Why_not_a_new_Compositor?), I found using the following command would create a new, blank session:


```
$ kwin_wayland --xwayland
```

This is almost what I want, I just want to run spotify in it. This is where I started having trouble. I found that `spotify-launcher` has a separate config file. I wasn't sure how to configure it though, and I also wasn't sure what `DISPLAY` to pass it when I run it. So I looked at the options for `kwin` and found the very useful `applications` option that lets you start applications there. Seemed exactly like what I wanted.

# Result

With that, I got the following:
 
```
$ kwin_wayland --xwayland applications spotify-launcher

```
I can click fullscreen and it is stuck to the size of the window. Pretty neat.

![Playing Superclean in Spotify fullscreen mode but its not fullscreen](/kde/kwin/banger.png)
