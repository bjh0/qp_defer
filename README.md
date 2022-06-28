# QP_DEFER
A C project in VS for playing with the defer functionality in QP Framework.

# DESCRIPTION
The QP Framework provides a 'defer' state pattern which allows the processing of chosen incoming events to be deferred until a later time.  An example where this is useful is when an event, received in an idle state, puts the state machine into a 'busy' state where it is doing some processing of an event, potentially waiting for other events to occur.  But then, new events received should be held off until the processing is complete.  And when the state machine returns to idle after processing, the deferred events shall be processed.

This project is an example of this functionality.  It is based on the standard example provided by QP but I added my own events, made them all manual (injected via the keyboard) so that the user can control which events occur at which times, and I used different types of events to make sure that the same queue can be used for all of the deferred events that come in.

Finally, I built it all in Visual Studio which allows for easier debugging and testing.

# PRE-REQUISITES
This example assumes you have the QP bundle installed in the standard directory on Windows (C:/qp).

# BUILD
To build this project you must ensure that Visual Studio is set to an x86 build profile.

# USAGE
The example supports three request events which simulate typical I2C communications.  You can make a DEVICE_DETECT request (d), a DEVICE_READ request (r), or a DEVICE_WRITE request (w).
When a request is made the state machine goes into the processing state for that event.  And here it basically waits for you to tell it the processing is complete.  You can do this by sending the DEVICE_DETECTED event (D) or the DEVICE_READ_COMPLETE event (R) or the DEVICE_WRITE_COMPLETE event (W).

If, while in one of the three processing states, a new request event is sent, then that event gets deferred and placed into a private queue until you complete the processing and it returns to the idle state.  On entry to the idle state a deferred event, if one is available, will immediately be processed.
