# Answer to debugging question
## Everett Robinson

> How would you go about locating the cause of a stack overflow or watchdog timer reset??

	Stack overflows

Stack overflows are common to C and C++, and the cause is usually a recursive function calling itself too many times. You see, each function call places several items on the stack, including the return pointer, the parameters passed to the function, and any local variables. A recursive function usually makes succeeding calls with a smaller and smaller piece of data, eventually winding up with a call that does not make a succeeding one. Where that final call is never made, that is usually the cause of a stack overflow.

The cause can sometimes be found by a simple examination of the code implementing the function. For more difficult cases, a debug log output can sometimes be used, printing the parameters passed to the function. Another way of finding this is to use a debugger, watching the passed parameters that way. For cases where many recursive calls are made (burdensome to watch), a check at the top of the procedure can be used that checks the function parameters to see if they have changed from the previous/parent call, along with a breakpoint within that check.

	Watchdog resets

A watchdog is a function that is periodically called (usually by an interrupt set from a hardware timer), which verifies that a loop is continuing to execute from top to bottom and hasn't gotten stuck. The watchdog uses a variable that is reset in the watchdog routine and set somewhere in the loop. If the watchdog sees the variable in its reset state, the loop has gotten stuck. Corrective measures can then be taken, which often are a reset of the CPU (usually a power-on reset).

If a debugger is available, a breakpoint can be set within the watchdog routine at the point of the execution of the corrective measure. The stack can then be examined. The position of the return pointer will inform where the loop has gotten stuck, and the cause will usually be obvious from that.

If a debugger is not available, it may be necessary to put debug statements in the loop at various points. One can zero in to find where the debugger is getting stuck. If debug statements are not available, then a global variable can be reserved, and statements setting a value can be inserted into the loop. Where the loop is getting stuck can be divined by observing the value when the watchdog trips.
