**Project description:** A multiplayer player card game, using 52 card deck, were players lay cards into the pile looking for pairs. If pairs are found first player to slap wins the pile. Exceptions are face cards, faces require the opposing player to lay the face value equivalent of cards down or until another face value is found or until a match is found. HTML and JavaScript were used.

### 1. Code Snippets

Function used to check if a card is a face card and change player turn. 

```javascript
function isCardFace(){
    //console.log("player turn: " + playerTurn);
    //console.log("your card: " + pile[0]); //used for testing
    var card = pile[0];
    
    //console.log("first letter: " + card.charAt(0)) //used for testing
    
    firstLetter = card.charAt(0);
    
    if(firstLetter === 'K' || firstLetter === 'Q'|| firstLetter === 'J' || firstLetter === 'A'){
            switch(firstLetter){
                case 'A':
                    isAce();
                    break;
                case 'J':
                    isJack();
                    break;
                case 'Q':
                    isQueen();
                    break;
                case 'K':
                    isKing();
                    break;
                default:
                    //console.log("no match");
        }
    } else {
        faceCard = false;
    }
    
    if (!faceCard && hasPreviousFaceCard && count === 0) {
        if (playerTurn === 0) {
            playerTurn = 1;
            } else {
                playerTurn = 0;
            }
        }
    else if (faceCard && hasPreviousFaceCard) {
     if (playerTurn === 0) {
        playerTurn = 1;
        } else {
            playerTurn = 0;
        }
    }
}
```

Function to select the first player to play a card.

```javascript
function whoFirst() {
    var random = Math.random();
    if (random < 0.5) {
        playerTurn = 0;
    } else {
        playerTurn = 1;
    }
}
```
