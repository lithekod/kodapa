note: see [lithekod/kodapa-2](https://github.com/lithekod/kodapa-2) for the new version using interaction commands.

# KODAPA
"Kontinuerlig och Ovärderlig Distribution Av Påminnelser och Agendor"

A bot to help the board with their meeting agenda and meeting
reminders.

## Features

- `!add <item>` adds an item to the agenda. Confirmation is sent in both Slack and
  Discord.
- `!agenda` prints the current agenda and who added each item.
- `!clear` clears the agenda.
- `!help` prints a short help message.

## Requirements

The binary itself depends on OpenSSL, as well as the usual suspects (glibc):

```
$ ldd target/debug/agenda-bot
        linux-vdso.so.1 (0x00007ffc353fd000)
        libssl.so.1.1 => /usr/lib/libssl.so.1.1 (0x00007f58987d2000)
        libcrypto.so.1.1 => /usr/lib/libcrypto.so.1.1 (0x00007f58984f4000)
        libdl.so.2 => /usr/lib/libdl.so.2 (0x00007f58984ee000)
        libpthread.so.0 => /usr/lib/libpthread.so.0 (0x00007f58984cc000)
        libgcc_s.so.1 => /usr/lib/libgcc_s.so.1 (0x00007f58984b2000)
        libc.so.6 => /usr/lib/libc.so.6 (0x00007f58982e9000)
        /lib64/ld-linux-x86-64.so.2 => /usr/lib64/ld-linux-x86-64.so.2 (0x00007f5899b1b000)
        libm.so.6 => /usr/lib/libm.so.6 (0x00007f58981a1000)
```

It has only been tested on Linux. macOS should work. Rust stable is needed to
compile.

## Building

In order to actually use the bot you need:

- Somewhere for it to live
- A Slack "classic" bot user
- A Discord bot user
- Necessary permissions to add bots to your Slack workspace and Discord server

Then, either pass the bot tokens as enviornment variables (`DISCORD_API_TOKEN`
and `SLACK_API_TOKEN`), or hard-code them into the binary (**NOT RECOMMENDED**
except for development purposes) by editing `src/discord.rs` and `src/slack.rs`.

Which channels the messages are sent to is currently specified via either
hard-coded constant values (again, not recommended, but at least not a security
issue here) or environment variables (`DISCORD_CHANNEL` and `SLACK_CHANNEL`). If
any of the two isn't set the bot will print a list of channels and their IDs
when starting so you can specify a channel.

The following shows all necessary steps needed to build and run the bot:

```shell
$ git clone https://github.com/lithekod/kodapa.git
$ cd kodapa
$ DISCORD_API_TOKEN=""     \ # fill
        SLACK_API_TOKEN="" \ # in
        DISCORD_CHANNEL="" \ # your
        SLACK_CHANNEL=""   \ # values
        cargo run
```

## Discord display names

In order to see Discord nicknames the bot needs the Presence Intent which can
be enabled on your Discord apps bot page.
