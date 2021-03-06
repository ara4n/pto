# Perpetually Talking Online

[![Build Status](https://travis-ci.org/tdfischer/pto.svg?branch=master)](https://travis-ci.org/tdfischer/pto)
[![Stories in Ready](https://badge.waffle.io/tdfischer/pto.png?label=ready&title=Ready)](https://waffle.io/tdfischer/pto)

An IRC to Matrix bridge.

This is different from the existing appservice on matrix.org. This work in
progress allows IRC users to join a matrix community. Its just a readme/vague
requirements document right now but code is being hacked on! Its for the
hackerspace community https://oob.systems/. Come join us in
#pto:oob.systems.

The idea being that one could point irssi at an IRC "daemon" behind a .onion
address, and have access to the channels that are local to a homeserver. Joining
\#the-oob would result in the user's matrix user joining \#the-oob:oob.systems, if
the IRCd is pointed to serve up the oob.systems namespace. Users can use SASL
auth to login with their existing oob.systems matrix account.

It would be impossible to join channels outside the homeserver for simplicity of
implementation, and really, this is about building a tight-knit community. One
should still be able to talk with everyone who is in the channel, including
users from outside the homeserver and handle various channel management tasks
such as kicks, bans, topics, etc.

This provides a *super* low level interface to onboarding new users to an
existing (or new!) Matrix community.

## Building this sucker

You'll need the following ingredients: 

- Rust >= 1.5.0: https://www.rust-lang.org/
- Cargo (any recent)

Once those two are installed, you can build PTO as follows:

  ``$ cargo build``

PTO can then be ran by specifying the domain to login at:

  ``$ cargo run matrix.org``

Specify a different URL to use a different matrix server.

Or the appropriate binary named ./target/\*/pto

To use a different address+port, use:

  ``$ cargo run matrix.org 0.0.0.0:4242``

You can also specify a full URL to use, such as when running on the same host:

  ``$ cargo run http://localhost:8000/_matrix/ 0.0.0.0:4242``

## Configuration

Currently configuration is limited to modifying hardcoded strings in various
places. Thank you for getting this far though! I would absolutely love a patch
<3

The following are hardcoded defaults:

- Listens on 127.0.0.1:8001 by default unless told otherwise
- Requires SSL for non-loopback addresses
- If SSL is used, it requires files named ./pto.crt and ./pto.key for a SSL
  certificate and key, respectively

PTO accepts two command line arguments:

  ``$ pto <hostname-or-url> [<listen-address:port>]``

``hostname-or-url`` can be a url such as ``https://matrix.org/\_matrix/``, or it can
just be a domain name such as ``matrix.org``. In the case of only using a domain
name, PTO will look up the \_matrix.\_tcp SRV record and use that if one exists.

## Usage

By default, PTO will listen on localhost:8001 for an IRC client to connect with
an appropriate username and password. The username and password supplied through
the IRC connection will be used to login to matrix.

With most clients, this is called your "ident" and "server password". SASL
authentication is currently unimplemented though patches are welcome and
appreciated.

PTO will only support logins to the server specified on the command line,
meaning your username is your matrix username. For example, if your login is
@alice:matrix.org, use 'alice' to login to PTO.

Guest support is currently unimplemented though both protocols support the idea
very well.

# TODO

Check out the Github issues for the project.
