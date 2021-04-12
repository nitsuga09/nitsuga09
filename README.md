from machine import Pin,I2C
from time import sleep_ms
import math
import machine

#Rasberry pi pico
led = machine.Pin(25, Pin.OUT)
i2c = I2C(0, scl = Pin(22), sda = Pin(21), freq = 400000)

# Creo las variables
buf = bytearray(100)

while (True):
    for i in range(len(buf)):
            buf[i] = 128 + int(127 * math.sin(2 * math.pi * i / len(buf)))
            i2c.writeto(0x61, buf[i])
            print(buf[i])
            sleep_ms(100)
