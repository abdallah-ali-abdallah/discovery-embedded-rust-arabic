# Serial communication



_This is what we'll be using. I hope your computer has one!_

Nah, don't worry. This connector, the DE-9, went out of fashion on PCs quite some time ago; it got replaced by the Universal Serial Bus (USB). We won't be dealing with the DE-9 connector itself but with the communication protocol that this cable is/was usually used for.

So what's this [_serial communication_](https://en.wikipedia.org/wiki/Asynchronous\_serial\_communication)? It's an _asynchronous_ communication protocol where two devices exchange data _serially_, as in one bit at a time, using two data lines (plus a common ground). The protocol is asynchronous in the sense that neither of the shared lines carries a clock signal. Instead, both parties must agree on how fast data will be sent along the wire _before_ the communication occurs. This protocol allows _duplex_ communication as data can be sent from A to B and from B to A simultaneously.

We'll be using this protocol to exchange data between the microcontroller and your computer. Now you might be asking yourself why exactly we aren't using RTT for this like we did before. RTT is a protocol that is meant to be used solely for debugging. You will most definitely not be able to find a device that actually uses RTT to communicate with some other device in production. However, serial communication is used quite often. For example some GPS receivers send the positioning information they receive via serial communication.

The next practical question you probably want to ask is: How fast can we send data through this protocol?

This protocol works with frames. Each frame has one _start_ bit, 5 to 9 bits of payload (data) and 1 to 2 _stop bits_. The speed of the protocol is known as _baud rate_ and it's quoted in bits per second (bps). Common baud rates are: 9600, 19200, 38400, 57600 and 115200 bps.

To actually answer the question: With a common configuration of 1 start bit, 8 bits of data, 1 stop bit and a baud rate of 115200 bps one can, in theory, send 11,520 frames per second. Since each one frame carries a byte of data that results in a data rate of 11.52 KB/s. In practice, the data rate will probably be lower because of processing times on the slower side of the communication (the microcontroller).

Today's computers don't support the serial communication protocol. So you can't directly connect your computer to the microcontroller. Luckily for us though, the debug probe on the micro:bit has a so-called USB-to-serial converter. This means that the converter will sit between the two and expose a serial interface to the microcontroller and a USB interface to your computer. The microcontroller will see your computer as another serial device and your computer will see the microcontroller as a virtual serial device.

Now, let's get familiar with the serial module and the serial communication tools that your OS offers. Pick a route:

* [\*nix](nix-tooling.md)
* [Windows](windows-tooling.md)
