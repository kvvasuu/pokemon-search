# Pokémon Search App.

## General info

It started as a certification project from freeCodeCamp.org - **"Build a Pokémon Search App"**...
...But I did much more than was required to pass and then remake it using Vue...
...Then added more and more :D

In the application, we enter the name or ID of the Pokémon. After pressing the "search" button, the application sends a request to the API. If it finds the right Pokemon, it is displayed on the website:

- Name, ID - \* _ID must be between 1-1025 or 10001-10277._ \*
- Weight, Height
- Appearance
- Types
- Items \* _(if available)_ \*

You can play sound of Pokémon by clicking on it.

If Pokémon has any items on hand they will be displayed. \* _(i.e. "Ditto" has 2 items - try it yourself)_ \*

A table with statistics is displayed below.

If it doesn't find a Pokémon, it displays the message "Pokémon not found"

## Technologies:

- Vue
- Font Awesome
- PokéAPI- https://pokeapi.co/

## Setup

```
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run all tests
npm test
```
