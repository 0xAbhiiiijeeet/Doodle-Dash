# Doodle Dash

A real-time multiplayer drawing and guessing game. Players join a room, take turns drawing a secret word, and everyone else tries to guess it in the chat. Faster guesses earn more points.

## Features

- Create a room with a name, player limit and number of rounds, or join an existing room by name
- Waiting lobby that fills up before the game starts
- Shared drawing canvas that updates live for every player
- Brush color picker, stroke width control and a clear-canvas button
- Live chat where guesses are checked against the secret word
- Turn and round rotation, with a random word for every turn
- Speed-based scoring and a live scoreboard drawer
- Final leaderboard when all rounds are finished
- Handles players leaving the room mid-game

## Tech Stack

| Part | Technologies |
| --- | --- |
| App | Flutter, Dart, CustomPainter, socket_io_client |
| Server | Node.js, Express, Socket.IO |
| Database | MongoDB with Mongoose |

## How It Works

- The Flutter app talks to the Node server over Socket.IO events such as `create-game`, `join-game`, `paint`, `msg` and `change-turn`.
- Each room is stored in MongoDB with its players, current word, round and turn.
- Drawing strokes are sent to the server and broadcast to every player in the room, so everyone sees the same canvas.
- When a guess matches the word, the guesser earns `round(200 / seconds taken * 10)` points.

## Project Structure

```
lib/        Flutter app (screens, drawing painter, scoreboard, widgets)
server/     Node + Express + Socket.IO server
  models/   Mongoose schemas for Room and Player
  api/      Random word generator
```

## Getting Started

### Server

```bash
cd server
npm install
npm run dev
```

The server listens on port `3000`. Set your own MongoDB connection string in `server/index.js` (the `DB` variable) before running.

### Flutter app

```bash
flutter pub get
flutter run
```

The server address is set in `lib/paint_screen.dart`. Replace it with your computer's IP address, and make sure the phone and the server are on the same network.
