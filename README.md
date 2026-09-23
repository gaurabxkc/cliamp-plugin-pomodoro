# cliamp-plugin-pomodoro

A focus timer for [cliamp](https://github.com/bjarneo/cliamp), for working to music.

Press **H** to start a session. Music plays through the focus phase and **pauses during breaks**, so the silence is what tells you to stop, no timer to watch. After four rounds the break is a long one.

It is also a visualizer: a full-width countdown clock instead of the spectrum.

## Install

```sh
cliamp plugins install gaurabxkc/cliamp-plugin-pomodoro
```

Restart cliamp and press **H**.

## Keys

| Key | Action |
|---|---|
| `H` | Start or stop a session |
| `)` | Add a minute to the running phase |
| `(` | Take a minute off (never below one minute) |
| `v` / `Ctrl+V` | Switch the visualizer to `pomodoro` for the countdown clock |
| `V` | Full-screen clock |

Only the running phase changes when you adjust it; the next one uses its configured length.

From a shell:

```sh
cliamp plugins call pomodoro start
cliamp plugins call pomodoro status   # phase, time left, all-time count
cliamp plugins call pomodoro stop
```

## Settings

All optional, in `~/.config/cliamp/config.toml`:

```toml
[plugins.pomodoro]
work_minutes             = 25
break_minutes            = 5
long_break_minutes       = 15
rounds_before_long_break = 4
adjust_minutes           = 1     # step for ( and )
cell_aspect              = 2.0   # your terminal's cell height ÷ width
```

`cell_aspect` keeps the clock's digits from looking stretched. 2.0 suits most terminals; raise it for a narrow font or extra line spacing.

## The clock

The countdown is drawn with half-block characters at whatever size the panel allows, with a progress line underneath: bright for elapsed, dim for remaining. Raise `vis_rows` in your config for a bigger inline clock, or press `V` for the whole window. Below about 6 rows it falls back to plain text.

If you pause the music yourself during a break, the plugin leaves it paused: it only resumes playback it paused itself. Completed rounds are counted in the plugin store, so the all-time total survives restarts.

## Requirements

cliamp with [#525](https://github.com/bjarneo/cliamp/pull/525) (uppercase plugin keys) for `H`. Until that is released, start sessions with `cliamp plugins call pomodoro start`.

## License

MIT
