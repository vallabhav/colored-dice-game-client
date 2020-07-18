# Colored Dice Game Client

This is a simple online game build on VueJS where one can play with his/her friend or with a computer online. There is a colored dice, contains 6 unique colors at each side.
Each player randomly gets 3 color buckets and each bucket can hold 'x' number of colors, to make it simple by default it will be 3 in each bucket. 
For example if the dice colors are (Red, Yellow, Blue, Green, Orange, Purple), lets say if player1 gets colors Red, Yellow, Blue colored buckets with 3 different objects(by default) then player2 will get other 3 colors(Green, Orange, Purple).

If player1 rolls the dice and gets Green then one of the object in player2 gets eliminated and player1 gets another chance as he hit otherwise the chance goes to player2 to roll the dice. The player who clears the opponent's colored objects first be the winner of the game and then the game is over.

The game dashborad looks like this: 
![Game Board](https://github.com/vallabhav/colored-dice-game-client/blob/master/blob/images/dashboard.JPG?raw=true)

To run this application, the game server app should be running, it can be found at:
https://github.com/vallabhav/colored-dice-game-server.git

## Project setup
```
npm install
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Compiles and run in development environment
```
npm run serve
```

The game client can be accessed at  http://localhost:8080/







