# mpptCommander
Python library for querying the Renogy Commander MPPT solar controller


The first question you might ask is why I wrote this.  The answer is that I
hadn't found the one here https://github.com/kasbert/epsolar-tracer yet. The
other half of the answer is that I probably would have anyway since I had
never used modbus before. I'm always up for learning new things. There are
some interesting similarities between this library and the epsolar-tracer,
namely the Register data type and it's data fields. They are not 100%
compatible but Jarkko Sonninen and I obviously thought similarly about the
problem space.  Once I found his project, I ended up grabbing some of the
register text since the data sheet was difficult to copy from due to
selection order in the pdf.  No code from the project was used in this
project.  I chose an immutable Register and a more functional approach for
mpptCommander.

One important distinction is that this library does not use pymodbus. So there
is one less dependency to deal with. This library is also slightly faster than
tracer (don't quote me on that, I didn't measure it, but it seems faster).
Meaning that it gets more data faster over 485. Clearly it's not the 485 speed
that's different.  There must be some overhead in pymodbus. It takes quite a 
while to gather all the fields over modbus when running at 115200.

I started this project to help out a HAM radio friend of mine.  He has been using
the Renogy controllers for some time now and he's a Linux user.  He wanted a way 
to query the controller through Linux.  I borrowed a Commander, a solar panel,
and a battery from him and off I went to work on this.

There will most likely be a UI for this soon enough.

The major milestone for the first official release is to have the library return
immutable return values that contain all the data that can be received from
a query of the Commander.  Some calls return a plethora of information in one
call using a bitfield.  Others return just one integer value.
