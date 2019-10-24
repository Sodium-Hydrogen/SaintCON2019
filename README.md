## SAINTCON Labs Minibadge ##
<img scr="readmeFiles/labs.jpeg" width="100px" />

### Things you'll need ###
* bus pirate
* SAINTCON Labs minibadge
* Computer with usb port

### Walkthrough ###
1. Connect to the bus pirate. This can be done by following [this guide]. (You shouldn't need to install any drivers)
2. Place the minibadge in the minibadge spot on the bus pirate. **Make Sure the switch by the minibadge is set to I2c**
3. Enter the I2C mode of the bus priate
   * This can be done by typing `m4` so your line should look like `Hiz> m4`
   * Press enter twice
4. To make sure the device is connected properly type `(1)` which should return 
```
Searching I2C address space. Found devices at:
0xA0(0x50 W) 0xA1(0x50 R)

I2C>
```
_If it doesn't there might be a slodering problem on the chip_


5. To set the message you need to send a start `[` then the write address `0xA0` followed by the memory location `0 0` and the stop bit `]`
   * `[0xA0 0 0]`
   * Then send `[ 0xA0 2` 0x2 or 2 is the byte indicating that we have a text message
   * Now enter the length of your message, etc for _Hello World_ it would be __11__
   * Now type your message inside `"`, etc `"Hello World"`
   * All this should look like: `[0xA0 0 0][0xA0 2 11 "Hello World]`
   * Send the commands
6. To double check it send you can reset the memory location `[0xA0 0 0]`
   * read from the minibadge by typing `[0xA1 r:#]` where # is the number of time you want to read
   * Your output will look something like:
```
I2C START BIT
WRITE: 0xA0 ACK
WRITE: 0x00 ACK
WRITE: 0x00 ACK
I2C STOP BIT
I2C START BIT
WRITE: 0xA1 ACK
READ: 0x02  ACK 0x0B  ACK 0x48  ACK 0x65  ACK 0x6C  ACK 0x6C  ACK 0x6F  ACK 0x20
ACK 0x57  ACK 0x6F  ACK 0x72  ACK 0x6C  ACK 0x64
NACK
I2C STOP BIT
I2C>
```
7. You can set the output mode to text by entering the command `o4` and resend the command to see the text. `o1` will reset the output mode.
8. Once you have everything set the way you want you can plug it into your badge and restart your badge.

*The minibadge writes once every 30 seconds*

# **Bring the Bus pirate back to SAINTCON Labs once you have your message set** #






[this guide]:https://learn.sparkfun.com/tutorials/terminal-basics/connecting-to-your-device
