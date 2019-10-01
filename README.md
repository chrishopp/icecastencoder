# Icecast encoder setup
Basic Icecast streaming server encoder setup on Lubuntu VM using broadcast using this tool (butt).
This is applicable to a bare metal install of an OS as well with minor modifications.

This guide is meant as a basic starting point to setup an encoder to feed an Icecast server. I utilize ESXi for my setup, but an OS install on an individual computer would work as well. I use consumer sound cards, but most any sound card would do, including onboard sound from most motherboards and broadcast soundcards from manufacturers like AudioScience. ESXi passthrough is utilized to accomadate multiple sound cards in one host machine. I run Lubuntu installs, but that is simply a preference of the lightweight OS and Debian over Fedora. Most any flavor can be setup to run this encoder if you're knowledgable with a particular one. This guide will focus on Lubuntu on an ESXi host.

## Starting Notes
1. This guide assumes basic shell knowledge.
2. These instructions are based on a GUI install. A shell only version is a future project. There aren't many differences aside from the text editor chosen to edit the configuration files. Most everything else is already done in shell only.
3. These instructions will get the basic encoder, butt, setup and running. Proper setup of the configuration files is currently outside the scope of this guide. The latest documentation of butt can be found at https://danielnoethen.de/butt/manual.html.

## OS Specific instructions
1. [Lubuntu](https://github.com/chrishopp/icecastencoder/tree/master/Lubuntu)

## Coming Up
1. Shell only guide and hints.
2. Discussion of configuration file.