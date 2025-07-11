This project has been created as a coding challenge for a front-end developer.

Included is a small and simple web server, built in NodeJS with Express.

Please make sure that a recent version of NodeJS is installed on your machine.

To start the web server, navigate to the backend directory and issue:
```
$ node app.js
```
The web server should then be accessable at `localhost:3000`.

The server offers two endpoints: **game** and **game-action**.

This is a tic-tac-toe game.

## GET /game?id={game_id}

Once the server is running, it will begin storing "games" in memory.

A game can be defined as:

```javascript
{
    id: string;
    data: (string | null)[][]
}
```

_NOTE: The data array is always 3 x 3_

**GET /game** requires that you pass a **game_id** parameter.

This parameter is any string that you wish to use to specify a game.

If a game by that id does not exist, **one by that id will be created.**

The `game` by that id will then be returned.

Example Request:

```
GET /game?id=Game1
```

Example Response:

```
{
    id: 'Game1'
    data: [
        [null, null, null],
        [null, null, null],
        [null, null, null]
    ]
}
```

## POST /game-action

**POST /game-action** requires that you pass four parameters:

* id
* player (must be either X or O)
* x (integer between 0 and 2)
* y (integer between 0 and 2)

If the parameters are valid, a game by the provided **game_id** exists, and the position requested is not already taken, the game data will be updated to set the provided player in the requested position.

Upon success, the `game` will be returned.

Example Request:

```
POST /game-action
PAYLOAD: {
    id: 'Game1',
    player: 'X',
    x: 0,
    y: 0
}
```

Example Response:

```
{
    id: 'Game1',
    data: [
        ['X', null, null],
        [null, null, null],
        [null, null, null]
    ]
}
```

## Goals

To complete this code test, please create a directory called `frontend` at the base of the repository.

Once created, please create an application that allows a user to create a new tic-tac-toe game, join an existing tic-tac-toe game, and play a tic-tac-toe game.

This can simply be a one page application, where the URL is **/game/{game_id}/{ player_id }**.

If you have any questions, please reach out for help.

## Optional Goals (Bonus points)
* Determine when a game has been completed
   * Either in the web application or the server, determine when a game has been won, display the winner, and prevent any further actions to the game.
* List the existing game
   * Create a new endpoint to serve the list of existing games by id. Show the list in the frontend application and allow a user to join a game by some sort of click action on the list item.
* Allow definable game size
   * To be restful, our game create should not exist in the GET endpoint. Break out this functionality into a separate POST request. If the game by the provded game-id does not exist, return a 404
   * When creating a game using the POST endpoint, accept a single field in the payload: **size**. This is an integer with a minimum of three. If a value less than 3 is provided, or if the field is omitted, return a 400 Bad Request error.
   * Alter the game completion validation logic to properly handle a game of any size. 
