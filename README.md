# Pokémon Search App.
![App demo](https://raw.githubusercontent.com/kvvasuu/pokemon-search/master/demo.png "App demo")

## General info

It started as a certification project from freeCodeCamp.org - **"Build a Pokémon Search App"**...
But I did way more than what was required to pass the exam and then remake it with Vue...
Then added even more and more...
Then finally deployed on Netlify - **https://kvvasu-pokesearch.netlify.app/**

In the application, we enter the Pokémon's name or ID. After pressing the "search" button, the application sends a request to the API. if a suitable Pokemon is found, it will be displayed on the website:

- Name, ID - _The ID must be in the range 1-1025 or 10001-10277_
- Weight, Height
- Appearance
- Types
- Items - _(if available)_

By pressing on a Pokémon you can change its appearance to "Shiny"
and play its sound. You can mute sounds by pressing the speaker icon
in the upper right corner, above the "info" icon.

If the Pokémon has any items, they will be displayed. By clicking on
an item you can check its details. _(i.e. "Ditto" has 2 items - try it yourself)_

A table with statistics is displayed below.

If it doesn't find a Pokémon, it displays the message "Pokémon not found"

The information is mostly based on video game franchise.
Data is obtained from PokeAPI - https://pokeapi.co/

## Technologies:

- Vue
- Font Awesome
- PokéAPI

## Setup

```
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run serve

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run all tests
npm test
```
