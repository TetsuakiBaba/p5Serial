# p5.serial
p5.serial is a simple serial communication library for p5.js, which is using web serial on the backend, and designed to be easy to use and to work with the p5.js library. 

> [!CAUTION]
> This repository is currently under construction and may be frequently updated.

## CDN
```
<script src="https://cdn.jsdelivr.net/gh/TetsuakiBaba/p5.serial.js/p5.serial.js" type="text/javascript"></script>
```

## Getting started with p5.js editor
  * https://editor.p5js.org/tetsuakibaba/sketches/EgLpDNrFq

## Getting Started
First of all, please upload the sketch to your arduino device. 
```cpp
void setup() {
  Serial.begin(9600);
}
int count = 0;
void loop() {
  Serial.writeByte(count);
  count++;
  delay(100);
}
```
### minimal style
Go to [DEMO page](https://tetsuakibaba.github.io/p5.serial/samples/minimal.html) and click the connect button. You will see the serial value on the page.

`index.html`
```html:index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
</head>
<body>
    <main>
        <button onclick="mystart()">connect</button><br>
        <p>
            Serial value:
            <span id="serial_value"></span>
        </p>
    </main>
    <script src="https://cdn.jsdelivr.net/gh/TetsuakiBaba/p5.serial.js/p5.serial.js" type="text/javascript"></script>
    <script src="sketch.js"></script>
  </body>
</html>

    <script>
        let serial = new Serial();
        function mystart() {
            serial.begin();
            serial.gotByte = function (value) {
                document.querySelector('#serial_value').textContent = value;
            }
        }
    </script>
</body>
</html>
```

## API
### Serial class
#### `Serial()`
Create a new Serial object.
```javascript
let serial = new Serial();
```
#### `Serial.begin()`
Open the serial port.
```javascript
serial.begin();
```

#### `Serial.close()`
Close the serial port.
```javascript
serial.close();
```

#### `Serial.gotByte()`
This function is called when a byte is received.
```javascript
serial.gotByte = function(value) {
    console.log(value);
}
```

#### `Serial.gotBytes()`
This function is called when bytes are received.
```javascript
serial.gotBytes = function(values) {
    console.log(values);
}
```

#### `Serial.gotCSV()`
This function is called when a CSV string is received. We recommend using this function when you want to receive multiple values at once.

```javascript
serial.gotBytes = function(values) {
    // if you send println('hello,world') from arduino, values is an array of number. ex) ['hello', 'world']    
    for( v of values){
        console.log(v); // hello, world
    }
}
```

#### `Serial.writeByte()`
Write a byte to the serial port.
```javascript
serial.writeByte(0x01);
```

#### `Serial.writeBytes()`
Write bytes to the serial port.
```javascript
serial.writeBytes([0x01, 0x02, 0x03]);
```

#### `Serial.writeCSV()`
Write a CSV string to the serial port. We recommend using this function when you want to send multiple values at once.
```javascript
serial.writeCSV('hello,world'); // send arduino "hello,world\n"
```

## for Developers

### How to update API documentation
```bash
npm run generate-docs
```

