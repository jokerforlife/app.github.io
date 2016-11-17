# Calculator

<html>
    <head>
        <title>
            Calculator
        </title>
        <script>
            document.addEventListener("mouseup", function(){
                setTimeout(function() {
                    
                    if (document.getElementById("box3").value < 0) {
                        document.getElementById("box3").style.color = "red";
                    } else {
                        document.getElementById("box3").style.color = "black";
                    }
                }, 1);
                document.getElementById("inputOutput").style.background = hexSet([255*Math.round(Math.random()), 255*Math.round(Math.random()), 255*Math.round(Math.random())], 2, '#');
            });
            function add() {
                var number1 = Number(document.getElementById("box1").value);
                var number2 = Number(document.getElementById("box2").value);
                document.getElementById("box3").value = number1 + number2;
            }
            function subtract() {
                var number1 = Number(document.getElementById("box1").value);
                var number2 = Number(document.getElementById("box2").value);
                document.getElementById("box3").value = number1 - number2;
            }
            function multiply() {
                var number1 = Number(document.getElementById("box1").value);
                var number2 = Number(document.getElementById("box2").value);
                document.getElementById("box3").value = number1 * number2;
            }
            function divide() {
                var number1 = Number(document.getElementById("box1").value);
                var number2 = Number(document.getElementById("box2").value);
                document.getElementById("box3").value = number1 / number2;
            }
            function exponent() {
                var number1 = Number(document.getElementById("box1").value);
                    // Number() rounds up
                var number2 = Number(document.getElementById("box2").value);
                var number3 = number1;
                if (number2 > 0) {
                    for (i = 1; i < number2; i++) {
                        number3 *= number1;
                    }
                    document.getElementById("box3").value = number3;
                } else if (number2 == 0) {
                    document.getElementById("box3").value = 1;
                } else {
                    for (i = -1; i > number2; i--) {
                        number3 *= number1;
                    }
                    document.getElementById("box3").value = 1 / number3;
                }
            }
            function clearValue() {  // This can't be called "clear()".
                document.getElementById("box1").value = "";
                document.getElementById("box2").value = "";
                document.getElementById("box3").value = "";
                keys["39"] = true;
                setTimeout(function() {
                    keys["39"] = false;
                    keys["40"] = true;
                    setTimeout(function() {
                        keys["40"] = false;
                        keys["37"] = true;
                        setTimeout(function() {
                            keys["37"] = false;
                            keys["38"] = true;
                            setTimeout(function() {
                                keys["38"] = false;
                                keys["39"] = true;
                                setTimeout(function() {
                                    keys["39"] = false;
                                }, 1000);
                            }, 1100);
                        }, 2000);
                    }, 1100);
                }, 1000);
            }
            
            function hexSet(numberList, digits, prefix) {  // prefix is optional
                var result = "";
                for (var number in numberList) {  // When this is done with arrays, the variable is the index.
                    number = Math.round(numberList[number]);
                    number = number.toString(16);
                    while (number.length < digits) {
                        number = "0" + number;
                    }
                    result += number;
                }
                return (prefix || "") + result;
            }
            
            var intervals = {};
            var keys = {};
            var position = {left:0, top:-110}; // This should be the same as the left and top values for #dot.
            window.onload = function() {  // This is what runs when the page loads; equivalent to <body onload=aFunction()>
                intervals.checker = setInterval(keyResponse, 10);
            }
            document.onkeydown = function(event) {  // This is when a key is pressed down. This is continually called.
                keys[String(event.keyCode)] = true;
            }
            document.onkeyup = function(event) {  // This is when a key is let up.
                keys[String(event.keyCode)] = false;
            }
            function keyResponse() {
                for (var key in keys) {
                    if (keys[key] == true) {
                        switch(Number(key)) {
                            case 37:  // left arrow key is pressed
                                position.left--;
                                break;
                            case 38:  // up arrow key is pressed
                                position.top--;
                                break;
                            case 39:  // right arrow key is pressed
                                position.left++;
                                break;
                            case 40:  // down arrow key is pressed
                                position.top++;
                                break;
                        }
                    }
                }
                document.getElementById("dot").style.left = position.left/10.0 + "em";
                document.getElementById("dot").style.top = position.top/10.0 + "em";
            }
        </script>
        <style>
            body {
                text-align: center;
            }
            div {
                position: relative;
                margin: auto;
            }
            input {
                text-align: center;
            }
            table {
                text-align: center;
                margin: auto;
            }
            #inputOutput {
                background: blue;
                width: 15em;
                height: 15em;
                border: .1em solid black;
            }
            #box1 {
                width: 6em;
                position: absolute;
                top: 1em;
                left: 1em;
            }
            #box2 {
                width: 6em;
                position: absolute;
                top: 1em;
                right: 1em;
            }
            #box3 {
                width: 8em;
                position: absolute;
                bottom: 1em;
                left: 5em;
            }
            #dot {
                background: blue;
                width: 5em;
                height: 6.5em;
                border-radius: 1em;
            }
        </style>
    </head>
    <body>
        <h1>
            Calculator
        </h1>
        <div id="inputOutput">
            <input type="text" id="box1" placeholder="1st number">
            <input type="text" id="box2" placeholder="2nd number">
            <input type="text" id="box3" readonly="true" placeholder="Result">
        </div>
        <div id="dot">
            <table>
                <tr>
                    <td>
                        <button onClick="add()">+</button>
                    </td>
                    <td>
                        <button onClick="subtract()">-</button>
                    </td>
                </tr>
                <tr>
                    <td>
                        <button onClick="multiply()">*</button>
                    </td>
                    <td>
                        <button onClick="divide()">/</button>
                    </td>
                </tr>
                <tr>
                    <td colspan="2">
                        <button onClick="exponent()">^</button>
                    </td>
                </tr>
                <tr>
                    <td colspan="2">
                        <button onClick="clearValue()">Clear</button>
                    </td>
                </tr>
            </table>
        </div>
    </body>
</html>
