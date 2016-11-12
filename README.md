# periodicrun
Python library for running a loop periodically with ~100 microseconds accuracy.

This library provides functionality for periodic execution of a method with accurate timing. It is meant by accurate timing that periodicrun guaranties that the loop will run every x seconds with 100 microsends (default) accuracy.

periodicrun uses Python's built-in *sched* library to schedule the execution of the given method periodically.

Usage
-----
Simple usage:
Run the exampleLoop method every 0.1 seconds (100 milliseconds).
~~~~
import periodicrun from periodicrun

def exampleLoop():
    print "Execution time (microseconds): ", int(round( time.time()*1000000 ))

pr = periodicrun(0.1, exampleLoop)
pr.run()
~~~~
Output:
Notice that only last 2 digits are varying (100us accuracy).
~~~~
Execution time (microseconds):  1478978426936189
Execution time (microseconds):  1478978427036170
Execution time (microseconds):  1478978427136171
Execution time (microseconds):  1478978427236171
Execution time (microseconds):  1478978427336183
~~~~

Thread Usage
------------
You can run the method as a seperate thread instead. Don't forget to join the thread using join() method in periodicrun.

Just use *run_thread()* instead of *run()*.
~~~~
import periodicrun from periodicrun

def exampleLoop():
    print "Execution time (microseconds): ", int(round( time.time()*1000000 ))

pr = periodicrun(0.1, exampleLoop)
pr.run_thread()

print "This will be printed immediately."
pr.join()
~~~~
Output:
~~~~
This will be printed immediately.
Execution time (microseconds):  1478978802699747
Execution time (microseconds):  1478978802799736
Execution time (microseconds):  1478978802899732
Execution time (microseconds):  1478978802999735
Execution time (microseconds):  1478978803099742
~~~~

Configuration
-------------
There are several configuration while creating the periodicrun object.

periodicrun(period, loop, args=(), lifetime=0, accuracy=0.0001)
* period: required. Running period in seconds.
* loop: required. The method to be run periodically.
* args: optional. The arguments of the method to be run. Default: no argument
* lifetime: optional. The lifetime of the periodic loop in seconds. If it is defined and different than zero, the loop will stop after specified seconds. Otherwise it will run forever.
* accuracy: optional. The timing accuracy of the peridic loop. If you do not need higher accuracy you can use larger number to reduce the CPU usage. You can use smaller number for better accuracy but CPU may not be able to do so (It depends on the system specs). Default: 0.0001 (100 microseconds)

