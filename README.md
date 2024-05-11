# Sweeper_Track_Bot
# New repo code for mini project4

from machine import Pin,PWM #importing PIN and PWM
import time #importing time


# Defining  right and left IR digital pins as input
right_ir = Pin(27, Pin.IN)
left_ir = Pin(26, Pin.IN)

# Defining motor pins
motor1=Pin(5,Pin.OUT)
motor2=Pin(6,Pin.OUT)
motor3=Pin(7,Pin.OUT)
motor4=Pin(8,Pin.OUT)
# Defining enable pins and PWM object
enable1=PWM(Pin(3))
enable2=PWM(Pin(4))



# Defining frequency for enable pins
enable1.freq(1000)
enable2.freq(1000)

# Setting maximum duty cycle for maximum speed
enable1.duty_u16(65025)
enable2.duty_u16(65025)

# Forward
def move_forward():
    motor1.low()
    motor2.high()
    motor3.high()
    motor4.low()
    
# Backward
def move_backward():
    motor1.high()
    motor2.low()
    motor3.low()
    motor4.high()
    
#Turn Right
def turn_right():
    motor1.low()
    motor2.high()
    motor3.low()
    motor4.high()
    
#Turn Left
def turn_left():
    motor1.high()
    motor2.low()
    motor3.high()
    motor4.low()
   
#Stop
def stop():
    motor1.low()
    motor2.low()
    motor3.low()
    motor4.low()
    
while True:
    if right_ir.value() == 0 and left_ir.value() == 0:
        move_forward()
    elif right_ir.value() == 1 and left_ir.value() == 0:
        turn_right()
    elif right_ir.value() == 0 and left_ir.value() == 1:
        turn_left()
    else:
        stop()
        