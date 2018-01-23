---
layout: post
title:  "calculatorJS [doc]"
date:   2017-09-24
categories: projects, javascript, fcc
---
Documentation below was written as I went through building the calculator-- user stories are from [FCC](https://freecodecamp.org).

user stories:
  * can add, subtract, multiply and divide two numbers.
  * can clear the input field with a clear button.
  * can keep chaining mathematical operations together until I hit the equal button, and the calculator will tell me the correct output.

```
<script>
  $(document).ready(function() {

  })
</script>

^not having the above written correctly was preventing my button from working 
```
- - - 
```
<script>
 var calc = '';
    $('button').on("click", function() {
      calc += $(this).attr("value");
      console.log(calc);
    })
</script>
```
^not working initially due to having $('#buttons') that encompassed all buttons instead of the button tag itself (as in script above)

- - - 
```
<script>
  $(document).ready(function() {
    var entry = ''; // button inputs
    var sum = 0;    // calculation total
    
    // calc buttons
    $('button').on("click", function() {
      entry += $(this).attr("value");
      sum = eval(entry);
      
      $('.results').html(sum);
      $('.mem').html(entry);
      
    }); // end of button
</script>
```
^it is collecting inputs and calculating through the use of `eval(str)` 
added mem section to show inputs-- need alternative to eval (look in YDKJS)

also the use of equal is in progress right now only calculation is through eval

- - - 
```
<script>
  $(document).ready(function() {
    // var entry = ''; // button inputs
    // var sum = 0;    // calculation total

    // // calc buttons
    // $('button').on("click", function() {
    //   entry += $(this).attr("value"); 
    //   //sum = eval(entry);
      
    //   $('.results').html(sum);
    //   $('.mem').html(entry);   
    // }); // end of buttons
    
    var entry = '';
    var current = 0;
    var answer = '';

    // testing
    $('button').on("click", function() {
      entry += $(this).attr("value");
      console.log("entry: " + entry);  
    });
    
    $('#equals').on("click", function() {      
      equals();
      entry = answer;
    })

    function equals() {
      current = eval(entry);
      answer = current;
      console.log(answer);
    }
  }) // end of doc
</script>
```
^ started over w/ buttons and got equal working
I'd still like to have that auto update on operations done b4 equal sign as I had b4

- - - 
```
<script>
  $(document).ready(function() {
    // var entry = ''; // button inputs
    // var sum = 0;    // calculation total

    // // calc buttons
    // $('button').on("click", function() {
    //   entry += $(this).attr("value"); 
    //   //sum = eval(entry);
      
    //   $('.results').html(sum);
    //   $('.mem').html(entry);   
    // }); // end of buttons
    
    var entry = '';
    var current = 0;
    var answer = '';

    // testing
    $('button').on("click", function() {
      entry += $(this).attr("value");
      current = eval(entry);
    $('.results').html(current);
    $('.mem').html(entry); 
      console.log("entry: " + entry); 
    });
    
    $('#equals').on("click", function() {      
      equals();
      entry = answer;
    })

    function equals() { 
      answer = current;
      console.log(answer);
    } 
  }) // end of doc
</script>
```
^ its doing what I'd like (regarding auto calcs), but would like alternative to eval -- part 1
```
<script>
  $(document).ready(function() {
    // var entry = ''; // button inputs
    // var sum = 0;    // calculation total

    // // calc buttons
    // $('button').on("click", function() {
    //   entry += $(this).attr("value"); 
    //   //sum = eval(entry);
      
    //   $('.results').html(sum);
    //   $('.mem').html(entry);   
    // }); // end of buttons
    
    var entry = '';
    var current = 0;
    var answer = '';

    // testing
    $('button').on("click", function() {
      entry += $(this).attr("value"); 
      showCase();
      console.log("entry: " + entry); 
    });
    
    $('#equals').on("click", function() {      
      equals();
      entry = answer;
    })

    function equals() { 
      answer = current;
      console.log(answer);
    }

    function showCase() {
      current = eval(entry);
      $('.results').html(current);
      $('.mem').html(entry);
    }
  }) // end of doc
</script>
```
^ its doing what I'd like (regarding auto calcs), but would like alternative to eval -- part 2 => rewrote it using function to seperate the current calcs

- - - 
```
<script>
  $(document).ready(function() {
    // var entry = ''; // button inputs
    // var sum = 0;    // calculation total

    // // calc buttons
    // $('button').on("click", function() {
    //   entry += $(this).attr("value"); 
    //   //sum = eval(entry);
      
    //   $('.results').html(sum);
    //   $('.mem').html(entry);   
    // }); // end of buttons
    
    var defaultVal = 0;
    var entry = '';
    var current = 0;
    var answer = '';


    // testing
    $('button').on("click", function() {
      entry += $(this).attr("value"); 
      showCase();
      console.log("entry: " + entry); 
    });
    
    $('#equals').on("click", function() {      
      equals();
      entry = answer;
    });

    $('#ac').on("click", function() { 
      allClear();
    });

    $('#c').on("click", function() {
      clearButton(); 
    })

    function equals() { 
      answer = current;
      console.log(answer);
      $('.mem').html(answer);
    }

    function showCase() {
      current = eval(entry);
      $('.results').html(current);
      $('.mem').html(entry);
    }

    function allClear() {
      entry = '';    
      $('.results').html(defaultVal);
      $('.mem').html(defaultVal);
    }

    function clearButton() {
      var newEntry = entry.substr(0, entry.length-1);
      //console.log(newEntry);
      entry = newEntry;
      console.log(entry);
      $('.mem').html(entry);
    }
  }) // end of doc
</script>
```
^clear buttons
```
<div class="container">
  <div class="main"> 
    <div class="black-top"></div>
      <div class="display">
        <br /><br />
        <span class="model">CASIO pocket-8S</span><br />
        <span class="title"><small>ELECTRONIC CALCULATOR</small></span>
        <br /><br /><br />
        <span class="results">0</span>
        <br /><br /><br />
        <span class="mem"><small>0</small></span>
      </div> <!-- end of display -->
      <div id="buttons">
        <button id="solar">o |||</button>
        <button id="ac" value=''>AC</button>
        <button id="c" value=''>C</button>
        <button id="percent" value='%'>%</button>
        <button class="num" id="seven" value='7'>7</button>
        <button class="num" id="eight" value='8'>8</button>
        <button class="num" id="nine" value='9'>9</button>
        <button class="operation" id="divide" value='/'>/</button>
        <button class="num" id="four" value='4'>4</button>
        <button class="num" id="five" value='5'>5</button>
        <button class="num" id="six" value='6'>6</button>
        <button class="operation" id="multiply"value='*'>x</button>
        <button class="num" id="one" value='1'>1</button>
        <button class="num" id="two" value='2'>2</button>
        <button class="num" id="three" value='3'>3</button>
        <button class="num" id="sub" value='-'>-</button>
        <button class="num" id="zero" value='0'>0</button>
        <button id="deci" value='.'>.</button>
        <button id="equals" value=''>=</button>
        <button class="operation" id="add" value='+'>+</button>
      </div> <!-- end of buttons -->
    <div class="black-bottom"></div>  
  </div> <!-- end of main --> 
</div><!-- end of container -->
```
^ cleaned up html 
```
@import url('https://fonts.googleapis.com/css?family=Coda:400|Electrolize|Inconsolata');

.main {
  width: 350px;
  height: 650px;
  background-color: #acacac;
  /* offset-x | offset-y | blur-radius | color */
  box-shadow: 15px 10px 15px -3px rgba(0, 0, 0, 0.8), inset -2px -5px 15px -2px rgba(0, 0, 0, 0.5);
  margin-left: 4px;
  border: 2px solid #929292;
  border-radius: 20px;
  -moz-border-radius: 20px;
  -webkit-border-radius: 20px;
  
}

.black-top,
.black-bottom {
  width: 350px;
  height: 25px;
  background-color: #262626; 
}

.black-top {
  border-radius: 17px 17px 0px 0px;
  margin-left: -0.5px;
}

.black-bottom {
  border-radius: 0px 0px 17px 17px;
  margin-top:36px;
  margin-left: -0.5px;
  border: 1px solid #262626;
  box-shadow: 15px 10px 15px -3px rgba(0, 0, 0, 0.3);
}

.display {
  width: 325px;
  height: 200px;
  background-color: #151412;
  margin: 55px 10px 0px 10px;
  border-radius: 30px 30px 20px 20px;
  border: 2px solid #3f3c37;
  text-align: center;
}

.model {
  color: white;
  text-decoration: underline;
  font-family: 'Coda', cursive;
  letter-spacing: 4px;
}

.title {
  font-family: 'Inconsolata', monospace;
}

.title, .results {
  color: teal;
}

.results {
  font-size: 30px;
  font-family: 'Electrolize', sans-serif;
  float: right;
  padding-right: 20px;
}

.mem {
  color: gray;
  font-family: 'Electrolize', sans-serif;
  float: right;
  padding-right: 20px;
}

button {
  color: white;
  border-radius: 7px;
}

#solar {
  width: 70px;
  height: 40px;
  margin-top: 25px;
  margin-left: 10px;
  background-color: #262626;
}

#ac, #c, #percent {
  width: 45px;
  height: 40px; 
  margin-left: 33px;
}

#ac, #c {
  background-color: orange;
}

#percent {
  background-color: skyblue;
  margin-left: 35px;
}

#seven, #eight, #nine, #divide,
#four, #five, #six, #multiply,
#one, #two, #three, #sub, 
#zero, #deci, #equals, #add {
  width: 45px;
  height: 40px;
  margin-top: 20px;
  margin-left: 34px;
}

#divide, #multiply, #sub, #add, #equals {
  background-color: gray;
}

#seven, #eight, #nine,
#four, #five, #six,
#one, #two, #three, 
#zero, #deci {
  background-color: #262626;
}
```
^ cleaned up css

- - - 
```
<script>
  $(document).ready(function() {
    // var entry = ''; // button inputs
    // var sum = 0;    // calculation total

    // // calc buttons
    // $('button').on("click", function() {
    //   entry += $(this).attr("value"); 
    //   //sum = eval(entry);
      
    //   $('.results').html(sum);
    //   $('.mem').html(entry);   
    // }); // end of buttons
    
    var defaultVal = 0;
    var entry = '';
    var current = 0;
    var answer = '';


    // testing
    $('button').on("click", function() {
      entry += $(this).attr("value");
      
      if(entry.includes("//") || entry.includes("**") || entry.includes("--") || entry.includes("++") || entry.includes("==") || entry.includes("..") || entry.includes("%%") ) {
        
        opCheck();
      }
      
      showCase();
      console.log("entry: " + entry);   
    });
    
    $('#equals').on("click", function() {      
      equals();
      entry = answer;
    });

    $('#ac').on("click", function() { 
      allClear();
    });

    $('#c').on("click", function() {
      clearButton(); 
    })

    $('#solar').on("click", function() {
      $('.mem').html("solar powered");
    })

    function equals() { 
      answer = current;
      // console.log(answer);
      $('.mem').html(answer);
    }

    function showCase() {
      current = eval(entry);
      $('.results').html(current);
      $('.mem').html(entry);
    }

    function allClear() {
      entry = '';    
      $('.results').html(defaultVal);
      $('.mem').html(defaultVal);
    }

    function clearButton() {
      var newEntry = entry.substr(0, entry.length-1);
      //console.log(newEntry);
      entry = newEntry;
      // console.log(entry);
      $('.mem').html(entry);
    }

    function opCheck() { 
      var filter = entry.replace(/[^A-Za-z0-9_]/, '');
      //console.log(filter);
       entry = filter;
      // console.log(entry);
       $('.mem').html(entry);  
    }
  }) // end of doc
</script>
```
^ solar button and consecutive operation doubles

- - - 
```
<script>
  $(document).ready(function() {
    
    var defaultVal = 0;
    var entry = '';
    var current = 0;
    var answer = '';

    $('button').on("click", function() {
      entry += $(this).attr("value");
      entry = entry.slice(0, 14); // caps digits
      
      if(entry.includes("//") || entry.includes("**") || entry.includes("--") || entry.includes("++") || entry.includes("==") || entry.includes("..") || entry.includes("%%") ) {
        
        opCheck();
      }
      
      showCase();
      // console.log("entry: " + entry);   
    });
    
    $('#equals').on("click", function() {      
      equals();
      entry = answer;
    });

    $('#ac').on("click", function() { 
      allClear();
    });

    $('#c').on("click", function() {
      clearButton(); 
    })

    $('#solar').on("click", function() {
      $('.mem').html("solar powered");
    })

    $('#percent').on("click", function() {
      getPercent();  
    })

    function equals() { 
      answer = current;
      // console.log(answer);
      $('.mem').html(answer);
    }

    function showCase() {
      current = eval(entry);
    
      $('.results').html(current);
      $('.mem').html(entry);
    }

    function allClear() {
      entry = '';    
      $('.results').html(defaultVal);
      $('.mem').html(defaultVal);
    }

    function clearButton() {
      var newEntry = entry.substr(0, entry.length-1);
      //console.log(newEntry);
      entry = newEntry;
      // console.log(entry);
      $('.mem').html(entry);
    }

    function opCheck() { 
      var filter = entry.replace(/[^A-Za-z0-9_]/, '');
      //console.log(filter);
       entry = filter;
      // console.log(entry);
       $('.mem').html(entry);  
    }

    function getPercent() {
      var convertToDecimal = entry.substr(-2);
        if(convertToDecimal < 10) {
          convertToDecimal = '0.0' + convertToDecimal;
        }
        else {
          convertToDecimal = '0.' + convertToDecimal;
        }
      
      // console.log(convertToDecimal);

      var edit = entry.substr(0, entry.length-2);
      // console.log("edit: " + edit);

      if(edit.includes('*')) {
        var updateMath = edit + convertToDecimal;
        entry = updateMath;
        // console.log(entry);
      }
      else if(edit.includes('+') || edit.includes('-')) {
        var multFirst = entry.substr(0, entry.length-3);
        updateMath = multFirst * convertToDecimal;
        $('.results').html(updateMath);
        updateMath = edit + updateMath;
        // console.log("update after calc: " + updateMath);
        entry = updateMath;
        // console.log(entry);
      }
      else {
        $('.results').html('error');
      }     
    }
  }) // end of doc
</script>
```
^ % functional-- current display however shoots off, needs fix

[fix current](https://stackoverflow.com/questions/7342957/how-do-you-round-to-1-decimal-place-in-javascript)

https://stackoverflow.com/questions/1726630/formatting-a-number-with-exactly-two-decimals-in-javascript
```
<script>
  function showCurrent() {
    current = eval(entry);
    var rounded = Math.round(current * 100) / 100;
    
    $('.results').html(rounded);
    $('.mem').html(entry);
  }
</script>
```

