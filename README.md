# Chess 

## Project Overview
This Chess game project is designed using the Model-View-Controller (MVC) architecture, with additional enhancements including text-based and graphical user interfaces. The game supports standard chess features, undo functionality, and AI opponents of varying difficulty. Due to Policy 71, our code cannot be posted publicly. This README provides a detailed overview of the project's architecture, features, and extensibility.


## Table of Contents
- Project Overview
- Project Structure
  - Model
  - View
  - Controller
- Design Patterns
  - MVC Architecture
  - Observer Pattern
- Features
- Design Decisions
  - Board Representation
  - Polymorphism and Inheritance
  - Circular Dependencies
  - Minimizing Coupling
  - Resilience to Change
- Future Work and Enhancements
- Lessons Learned

---

## Project Structure
Our project consists of three modules: Model, View, and Controller, following the MVC architecture. Here's a breakdown of the main components:

## Model
The Model holds the state of the game and represents the chessboard and pieces.

- Board: Represents the chessboard with a 2D vector of Square objects.
- Square: Holds a Piece and serves as an individual cell of the chessboard.
- Piece: A base class for all chess pieces.
  - Pawn, Knight, Bishop, Rook, Queen, King: Subclasses that inherit from Piece.
- Enum classes: Colour, PieceType, MoveType.
- Structs: Move, MoveInfo.

## View
The View module manages the visual representation of the game.
- Observer: Abstract class for implementing the observer pattern.
- TextDisplay: Displays the board state as ASCII text.
- GraphicsDisplay: Displays a graphical board using XWindow, with visuals inspired by chess.com.

## Controller
The Controller manages the game flow and user interactions.
- GameController: Manages the overall game logic (initialization, moves, and game state transitions).
- Player: Base class for players.
  - Human: For human players.
  - ComputerOne, ComputerTwo, ComputerThree, ComputerFour: For AI players with increasing difficulty.
Utility: botutil for AI computations.

## Design Patterns

### MVC Architecture
We use the MVC architecture to ensure separation of concerns:
- Model manages the game state (board, pieces).
- View handles rendering (text-based or graphical).
- Controller interacts with the Model to execute moves and update the View.
  
### Observer Pattern
We implemented the Observer Pattern for real-time updates of the visual display:
- Each Square on the board is an observable. When a piece is moved or captured, it notifies the attached TextDisplay or GraphicsDisplay observers.
- This ensures the board's visual representation always reflects the current game state.
  
## Features
- Real-Time Display: Visuals are updated immediately when a move is made.
- Text-Based Display: Simple ASCII representation of the board for easy debugging.
- Graphical Display: Colourful, chess.com-inspired graphical interface.
- Player vs Player: Play with another human or against AI.
- Multiple AI Levels: Choose from four AI levels, each with increasing difficulty.
- Undo Functionality: Players can undo moves, with support for unlimited undos.
- Checkmate and Stalemate Detection: Detects when the game is over.

## Design Decisions

### Board Representation
We initially considered storing the board as a 2D vector of Piece objects, but using "empty" pieces felt unintuitive. Instead, we introduced a Square class to represent each cell, which could either contain a piece or be empty. This approach allows for real-time updates and aligns well with our MVC structure.

### Polymorphism and Inheritance
Chess pieces have unique movement patterns, so we used inheritance and polymorphism. The Piece superclass defines the structure and methods for all pieces, and subclasses (e.g., Knight, Bishop) override the getValidMoves() method to return piece-specific moves.

### Circular Dependencies
We faced a circular dependency issue among Board, Square, and Piece. To solve this, we introduced an interface class, BoardInterface, which exposes the necessary methods for validating moves without creating direct dependencies between these classes.

### Minimizing Coupling
By defining clear responsibilities for each module and using interface classes (like BoardInterface), we reduced coupling between components. This makes the program more modular and easier to maintain.

### Resilience to Change
Our design adheres to the Single Responsibility Principle, ensuring that changes in one class do not propagate throughout the system. For example, adding a new piece type (e.g., a new knight variant) would only require modifications to the corresponding class without affecting the rest of the system.

## Future Work and Enhancements
Move Suggestions: Show all possible moves when a piece is selected.
More AI Levels: Add more sophisticated AI levels with advanced strategies.
Online Multiplayer: Add support for online chess games.
Undo All Moves: Extend the undo functionality to allow resetting the game entirely.

## Lessons Learned

### Team Development
Developing software as a team requires strong communication and meticulous planning. We learned the importance of:
- Frequent group discussions to clarify tasks and coordinate efforts.
- Effective bug resolution by leveraging multiple perspectives.
- Clear task division to minimize conflicts and maximize daily progress.
  
### Code Structure
If starting over, we would place even more emphasis on initial planning. In retrospect, better foresight could have helped avoid some challenges, such as circular dependencies, which took a full day to resolve.
