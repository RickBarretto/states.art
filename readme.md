<h1 align="center">
    <i>:states</i>
</h1>

<p align="center">
    <i>:states</i> is a basic
    <a href="https://en.wikipedia.org/wiki/Finite-state_machine">
        Finite State Machine (FSM)
    </a>
    package for the 
    <a href="https://github.com/arturo-lang/arturo/">
        Arturo Programming language
    </a>
    <br><br>
    <img 
        alt="Arturo logo" 
        width="20" 
        src="https://github.com/arturo-lang/arturo/raw/master/docs/images/logo.png#gh-light-mode-only"
    />
    <img 
        alt="Arturo logo" 
        width="20" 
        src="https://github.com/arturo-lang/arturo/raw/master/docs/images/logo-lightgray.png#gh-dark-mode-only" 
    />
</p>

## At a Glance

![Running states.art screenshot](./docs/running%20states-art%20screenshot.png)

## Inspiration

This package was highly inspired by [*Harrington Joseph*][harrington-twitter]'s [^harph] talk ["*When Booleans Are Not Enough... State Machines?*"][next-day-video] [^talk].
By consequence, this is inspired by the [pytransitions][pytransitions] package.

> [!TIP]
> If you want to know why you need a FSM, I recommend you to watch his talk first.

## Trying *:states*

Defining a finite state-machine is simple like that:

```art
import {states}!

turnstile: to :states ['locked [
    push        /  locked    ~>  locked
    push        /  unlocked  ~>  locked
    insertCoin  /  locked    ~>  unlocked
    insertCoin  /  unlocked  ~>  unlocked
]]
```

**Explanation**

* The first parameter is the initial state,
* The second parameter is the definition os the transitions,
  this must follow the following order: *event*, *source*, *fate*, being or not separated by symbols.
* You can choose what symbol to use to separate them, or even choose by don't use them, making this a trilema.

**Getting the current state**

To get the current state, you must call the `state` method:

```art
turnstile\state 
; => locked
```

**Transitioning between states**

There are two equivalent ways of transitioning between states, you can use `<fsm>/<event>` or `<fsm>\changeFrom '<event>`:

```art
turnstile\state                   
; => locked
turnstile\push                   
; => locked
turnstile\insertCoin             
; => unlocked
turnstile\insertCoin             
; => unlocked

turnstile\changeFrom 'push       
; => locked
turnstile\changeFrom 'insertCoin 
; => unlocked
```

---

> Background photo on ["At a Glance"](#at-a-glance) 
  by [Jack Anstey](https://unsplash.com/@jack_anstey?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) on [Unsplash](https://unsplash.com/photos/aerial-photography-of-road-zS4lUqLEiNA?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)

[^harph]: You can find him on [Twitter][harrington-twitter] or [Github][harrington-github] as @harph.

[^talk]: "*When Booleans Are Not Enough... State Machines?*" by *Harrington Joseph* can be found in two places, on the Channel [*Next Day Video*][next-day-channel] Presented on [*PyTexas 2019*][next-day-video] and on the Channel [*SF Python*][sf-python-channel] presented on [*SF Python Meetup Feb 2019*][sf-python-video].

[harrington-twitter]: https://x.com/harph
[harrington-github]: https://github.com/harph
[next-day-channel]: https://www.youtube.com/@NextDayVideo
[next-day-video]: https://youtu.be/I1Mzx_tSpew
[pytransitions]: https://github.com/pytransitions/transitions
[sf-python-channel]: https://www.youtube.com/@SFPython
[sf-python-video]: https://youtu.be/H25eAdwZYwg