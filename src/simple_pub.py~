#!/usr/bin/env python
import serial
import rospy
from geometry_msgs.msg import Twist
from geometry_msgs.msg import Vector3
import time


class VelPublisher(object):
	def __init__(self, serial_port="/dev/ttyUSB0"):
		self.s = serial.Serial(serial_port, 115200, timeout=1)
		self.serial_data = 0
		rospy.init_node('Simple_Vel_Publisher', anonymous = True)
		self.pub = rospy.Publisher("/cmd_vel",Twist, queue_size = 1 ) #Publicar en el topic	o
		
	def read_serial(self):
		data = chr(1)
		self.s.write(data)
		a =  self.s.readline()
		if not a =="":
			self.serial_data = int(a.split("\n")[0])
			self.data_conversion()
		return self.data_converted
	
	def data_conversion(self):
		self.data_converted = self.serial_data * 1.8/1023
		
			
			
def main():
	publisher  = VelPublisher()
	rate = rospy.Rate(10)
	while not rospy.is_shutdown():
		val  = publisher.read_serial()
		twist_msg = Twist(Vector3(val,0,0),Vector3(0,0,0))
		publisher.pub.publish(twist_msg)
		rate.sleep()	


if __name__ == '__main__':
	main()
				
'''
p = VelPublisher()
#time.sleep(3)
#for i in range(100):
t =True
try:
	while t:
		p.read_serial()
		time.sleep(0.1)
		#print "....."
except KeyboardInterrupt:
	t = False	
'''	
	
