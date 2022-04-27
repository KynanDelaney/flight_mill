# A library to use the ADC in the circuit with the Pi.
from gpiozero import MCP3208
import time
# A library to work with postgresql.
import psycopg2
import datetime

print("Establishing database connection.....")

# Not the most efficient way to do this, but the documentation was sparse and I'm bad at Python. :(
adc0 = MCP3208(channel = 0)
adc1 = MCP3208(channel = 1)
adc2 = MCP3208(channel = 2)
adc3 = MCP3208(channel = 3)
adc4 = MCP3208(channel = 4)
adc5 = MCP3208(channel = 5)
adc6 = MCP3208(channel = 6)
adc7 = MCP3208(channel = 7)

# Session number - must be updated for each script run. 
# Creates prompt in command line that must be addressed before data is collected.
x = int(input("Input Session number here: "))

"""
Description:
make a postgres connection and talk to an adc
Loop forever:
    Loop for a hundredth of a second:
        Insert raw data.
"""

# Mill name and login info are hard-coded here. This could be achieved with user input as with "session number" above.
# User input is more appropriate where more devices are in use. 
conn = psycopg2.connect(
    host="localhost",
    database="greenmill",
    user="pi",
    password="raspberry")

# "While True" seemed to need something to be printed/ an end argument to allow for loops to cycle properly.
# Database name could not come from user input here, unless the script is reworked to allow for some paste0() expression to be defined.
# I dont know how SQL would handle that.
with conn.cursor() as cur:
	while True:
		query  = "INSERT INTO green(session, channel_0, channel_1, channel_2, channel_3, channel_4, channel_5, channel_6, channel_7) VALUES(%s, %s, %s, %s, %s, %s, %s, %s, %s)" % (x,adc0.raw_value,adc1.raw_value,adc2.raw_value,adc3.raw_value,adc4.raw_value,adc5.raw_value,adc6.raw_value,adc7.raw_value)
		cursor = conn.cursor()
		try:
			cursor.execute(query)
			conn.commit()
			time.sleep(0.01)
		finally:
			print("He's Dead, Jim")
