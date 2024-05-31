PiClusterNode
Raspberry Pi Cluster node controller

Access cluster nodes for serial I/O or power cycle

This program is used with my Cluster controller board to control up to 8 Rpi cluster nodes
For use with Version 2 board (also works with V1, but power monitor unavailable)

Board V1 used 74HC138/74HC251 for serial I/O, and 74HC259 for power enables
fixed serial speed issue and delivered power enable persistance
Problem: no power state monitoring for nodes (is the node on or off?)

Board V2 added a second 74HC251 for direct monitoring of power enable lines.


A 74HC138 (for TX) and 74HC251 (for RX) (de)multiplexers for fanout of TX and RX UART signals
from Pi1 to nodes 2-8 (pi2 has fixed ttyAMA2 - ttyAMA10 to pi1)
One x 74HC259 addressable latch, driving the Enable lines of the DC/DC
converters powering the Pi boards. CLK and DATA lines on GPIO 17 and 18
GPIO pins 2, 3 and 4 are address lines 0, 1 and 2 for above signals
Serial1 pins from pi1 via (de)mulitplexers, to serial0 of cluster nodes

(Board V2) Addition of power monitor using a second 74HC251 connected to the power enable
outputs from the 74HC259, so as to sample the current power status of nodes.
Output of power monitor is GPIO 27 (was serial enable in previous board versions)

GPIO 2,3,4 are address select pins for I/O multiplexers
pin 2 = bit 0
pin 3 = bit 1
pin 4 = bit 2

GPIO 18 is power pin -  active HIGH = POWEROFF!
Power off signal is latched by GPIO 17 CLK pin pulsing low (active LOW)
GPIO 17 is power latch Clk pin - high latches value, low enables Data to selected output
GPIO 27 WAS serial enable, but now is INPUT from power monitor mpx.

