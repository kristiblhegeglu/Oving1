Oving1
======

Python

# Python 3.3.3 and 2.7.6
# python helloworld_python.py

from threading import Thread, Lock

i = 0



def adder():
    global i
    for x in range(0, 1000000):
        i += 1

        
def subtractor():
	
    global i
    for x in range(0,1000000):
        i -= 1


def main():
    adder_thr = Thread(target = adder)
    subtractor_thr = Thread(target = subtractor)
    adder_thr.start()    
    subtractor_thr.start()
	    
    for x in range(0, 50):
        print(i)
        adder_thr.join()
        adder_thr.join()
	    
        print("Done: " + str(i))


main()


Sanntidsprosjekt_2014
