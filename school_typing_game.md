**Project description:** A single player game were a player could try and type as many words as possible, only losing if a word went below the water line. Languages used were CSS, HTML, JavaScript and PHP.

### 1. Code Snippets

Function used to update the position of the word in the DOM.

```javascript
function myMove(wordNumber) {
    //added style to this -- alec
    var elem = document.getElementById('test'+wordNumber);
    
    /*can implement later if we want, it's for a faster paced game. It should work -- alec*/
    //var RATE_INTERVAL = 0.5;
    var rate = 30;  //current speed at which words drop -- alec
    //rate = rate + RATE_INTERVAL;
    
    var pos = 0 //starting position of words -- alec
    var h = window.innerHeight;     //dynamic window height, should adjust to YOUR screen --alec
    var id = setInterval(frame, rate);  //function not sure what it does --alec
    function frame() {
         if(pos >= h*.65){
             clearInterval(id);
             //call a endGame function -- alec
             endGame();
         }
        else if(gameOver != false){
                clearInterval(id);  //resets interval -- alec
                //endGame();
        }
         else{
             pos+=.5;
             //value;
             if(userWord.localeCompare(fiveWords[wordNumber-1].toUpperCase()) == 0){ //if user whole word matches a word
                 //var index1 = isMatch.findIndex(checkTrue);
                 //throws and infinite loop without value reset -- alec
                 //document.getElementById('myAnimation'+wordNumber).innerHTML = "";
                 //value = "";
                 pos = 0;
                 //fiveWords[wordNumber-1] = 
		 updateWord(wordNumber - 1);
		 console.log(fiveWords[wordNumber - 1]);
                 document.getElementById("myAnimation"+wordNumber).innerHTML = fiveWords[wordNumber-1]; //undoes highlight on correct word
                 
                 //reset value and userword fixes the first typing issue -- alec
                 value = "";
                 userWord = "";


                 //myMove(index + 1);
             }
             else{
                elem.style.transform = "translateY(" + pos + "px)"; //else move it down
             }
         }
     }
}
```




