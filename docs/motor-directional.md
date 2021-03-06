<!--remove-start-->

# Motor - Directional

<!--remove-end-->






### Breadboard for "Motor - Directional"



![docs/breadboard/motor-directional.png](breadboard/motor-directional.png)<br>

Fritzing diagram: [docs/breadboard/motor-directional.fzz](breadboard/motor-directional.fzz)

&nbsp;




Run with:
```bash
node eg/motor-directional.js
```


```javascript
var five = require("johnny-five"),
  board = new five.Board();

board.on("ready", function() {
  var motor;
  /*
    ArduMoto
      Motor A
        pwm: 3
        dir: 12

      Motor B
        pwm: 11
        dir: 13


    AdaFruit Motor Shield
      Motor A
        pwm: ?
        dir: ?

      Motor B
        pwm: ?
        dir: ?


    Bi-Directional Motors can be initialized by:

      new five.Motor([ 3, 12 ]);

    ...is the same as...

      new five.Motor({
        pins: [ 3, 12 ]
      });

    ...is the same as...

      new five.Motor({
        pins: {
          pwm: 3,
          dir: 12
        }
      });

   */


  motor = new five.Motor({
    pins: {
      pwm: 3,
      dir: 12
    }
  });




  board.repl.inject({
    motor: motor
  });

  motor.on("start", function() {
    console.log("start");
  });

  motor.on("stop", function() {
    console.log("automated stop on timer");
  });

  motor.on("forward", function() {
    console.log("forward");

    // demonstrate switching to reverse after 5 seconds
    board.wait(5000, function() {
      motor.reverse(50);
    });
  });

  motor.on("reverse", function() {
    console.log("reverse");

    // demonstrate stopping after 5 seconds
    board.wait(5000, function() {
      motor.stop();
    });
  });

  // set the motor going forward full speed
  motor.forward(255);
});

```








&nbsp;

<!--remove-start-->

## License
Copyright (c) 2012, 2013, 2014 Rick Waldron <waldron.rick@gmail.com>
Licensed under the MIT license.
Copyright (c) 2014, 2015 The Johnny-Five Contributors
Licensed under the MIT license.

<!--remove-end-->
