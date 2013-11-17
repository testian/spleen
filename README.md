spleen
======

a split screen emulator for games that don't natively support split screen, implemented as wayland compositor (and client), based on qtwayland

With wayland we get the building blocks to create highly-integrated multiseat solutions with zero need for configuration, as easy as playing split screen on your game console.

The difference here is that we'll enable you to play just ANY game split screen (Minecraft, Quake, ) and using whatever and how many controls you like (Gamepad, Joystick, Mouse, Keyboard, Wheel)

How it is going to work
=======================

spleen will start several instances of the game, running side by side, so the game does not need to be aware of splitting.

So one part is to have every game instance think it's in fullscreen mode while in reality it just has half or a quarter of your monitor, or monitor ensemble.
spleen takes care of that and will enable you to rearrange your windows, put them on other monitors.

The second part is the problem of assigning each gamepad/mouse/keyboard to the correct game instance on your screen in a flexible way and without maintaining any config files.

As soon as spleen is started in fullscreen, having at least 2 game instances running, input devices first need to be assigned to a window.

This happens by using one input devices own controls using the instrument best suited for navigation (arrow keys, WASD, joystick, mouse cursor or scroll wheel, Turn left/right) and a confirmation and cancellation key (Enter/Esc, A/B, Start/Back, LMB/RMB, Throttle/Brake).

Each input device decorates (not a window-decoration as we know it) a window with a unique combination of color and symbol.
The symbol reflects the type of input device to further ease association. Plus each color is assisted by a unique number.

Several input devices can be assigned to the same window, confirm twice to complete association.

As soon as all windows have both input devices associated AND got confirmed that input device association is complete, the input is from now on redirected to the game instance (Pointers are no longer able to leave the windows now).

Enjoy.

Agenda
======

Idea: 100%


Concept: 95%


Design & Architecture: 25%
- Decision to implement as a wayland compositor which at the same time is a client (nested)
- base it on qtwayland
- Target to include X11-games (not yet sure how, probably a separate X11-instance for every window - any suggestion?. Is the problem completely solvable with X11-technology instead?)
- Target not just games, but also applications
- Target to be added as plugin into at least one wayland session compositor (KWin is my favourite) and logind to avoid context switches and to reuse their awesome window management abilities

Proof of Concept: 0%
- this is the next thing I'm going to work on

Implementation: 0%
- functionality as above
- after association is completed, don't render, instead forward client windows as scanout buffers

Enhancements: 0%
- X11
- Restart reassociation
- Persistence
- Enable non-games, sessions
- Enable late attached input device to attach to a session autonomously or by being grabbed by one of the sessions

Integration: 0%
- Ship with a distro
- Ship as session compositor plugin
- Ship as system compositor plugin

Documentation: 5%
