# Program Analysis

The overall program can be split into 2 main sections.  There is a static class called **Program** and then a set of other classes. As Program is static it functions very much like a traditional procedural program.  The initial starting subroutine is **Main**.

## Other Classes

The program also has a number of *proper* classes.  The key ones are

- Player.  2 objects created,  one for each player
- HexGrid. 1 object created which represents the playing board

Other classes are 
- Piece.  This class is an outline class for a players piece.  It is used as a template for 3 other classes
    - BaronPiece
    - LESSPiece (Wood cutter)
    - PBDSPiece (Peat cutter)
    - Piece itself seems to be used for the Serf piece

- Tile.  Each object of this class represents a single board tile.  It is accessed via a list within a Grid object.

## Object Model

```mermaid

---
title: Baron Game
---
classDiagram
direction RL
class HexGrid {
    # tile : Tile[]  
    # pieces : Piece[] 
    ~ size : int
    ~ player1Turn : bool
    + HexGrid()
    + SetUpGridTerrain() void
    + AddPiece() void
    + ExecuteCommand() string
    + DestroyPiecesAndCountVPs() bool
    + GetGridAsString() string
    + GetPieceTypeInTile string
    - CheckTileIndexIsValid() bool
    - CheckPieceAndTileAreValid() bool
    - ExecuteCommandInTile() bool
    - ExecuteMoveCommand() int
    - ExecuteSpawnCommand() int
    - ExecuteUpgradeCommand() int
    - SetUpTiles() void
    - SetUpNeighbours() void
    - MovePiece() void
    - GetPieceTypeInTile() string
    - CreateBottomLine() string
    - CreateTopLine() string
    - CreateOddLine() string
    - CreateEvenLine() string


}

class Tile {
    # terrain : string
    # x,y,z : int  
    # pieceInTile : Piece 
    # neighbours : Tile[] 
    + Tile() 
    + GetPieceInTile() Piece 
    + GetTerrain() string
    + Getx() int
    + Gety() int
    + Getz() int
    + SetTerrain() void
    + SetPiece() void
    + AddToNeighbours() void
    + GetNeighbours() Tile[]
    + GetDistanceToTileT() int
}

class Piece {
    # destroyed : bool 
    # belongsToPlayer1 : bool
    # fuelCostOfMove  : int
    # VPValue : int
    # connectionsToDestroy : int
    # pieceType : string
    + Piece()
    + GetVPs() int
    + GetBelongsToPlayer1() bool
    + CheckMoveIsValid() int
    + DestroyPiece() void
    + GetPieceType() string
    + GetConnectionsNeededToDestroy() int
    + HasMethod() bool
}

class BaronPiece {
    + BaronPiece()
    + CheckMoveIsValid() int
}

class LESSPiece {
    + LESSPiece()
    + CheckMoveIsValid() int
    + Saw() int
}

class PBDSPiece {
    + PBDSPiece()
    + CheckMoveIsValid() int
    + Dig() int
}

class Player {
    # piecesInSupply : int
    # fuel : int
    # VPs : int
    # lumber : int
    # name : string
    + Player()
    + GetStateString() string
    + GetVPs() int
    + GetFuel() int
    + GetLumber() int
    + GetName() string
    + AddToVPs() void
    + UpdateFuel() void
    + UpdateLumber() void
    + GetPiecesInSupply() int
    + RemoveTileFromSupply() void
}

Piece <|-- BaronPiece : Inheritance
Piece <|-- LESSPiece : Inheritance
Piece <|-- PBDSPiece : Inheritance
HexGrid *-- Tile : Composition
HexGrid *-- Piece : Composition
Tile --> Piece : Association
```

## Detailed Documentation

### [Program Class](./Documentation%20of%20Class%20Program.md)  
### [HexGrid and Tile Classes](./Documentation%20of%20HexGrid%20and%20Tile%20Classes.md)  
### [Piece Classes](./Documentation%20of%20Piece%20Classes.md)
<br>
<br>
## Notes

1) The Piece class is the basis for the other piece classes which all inherit from it.  It is also used for the "Serf" piece.  
2) The playing pieces are held in an array (of class Piece) which is stored in the HexGrid object.  
3) A **references** to each Piece object is also stored in the relevant **Tile** object

