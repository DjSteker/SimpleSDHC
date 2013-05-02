SimpleSDHC
==========

A basic SD Card SPI interface in VHDL which supports SD V1, V2 and SDHC.
Addressing is by sector number (512byte blocks.)
CRCs are generated and checked, and CRCs are enabled on the SD Card.

The card interface consists of Clock, Select, MOSI, MISO and two optional signals: CardPresent and WriteProt.

The internal interface consists of:
clk (in) - 50Mhz (or lower) clock.  SPI clock is half of this (*)
addr (in) - The 32bit sector address to be transfered
sd_busy - Indicates whether the controller can accept a new command
reset (in) - To initialise the controller
sd_error (out) - Indicates that an error has occured during initialisation or the transfer
sd_error_code (out) - Provides more information on the error

Reading from the card:
rd (in) - Read trigger signal, must be asserted for the entire transfer
dout (out) - 8bit data coming from the card
dout_avail (out) - Indicates that data is present on dout
dout_taken (in) - Indicates that data out has been accepted

Writing to the card:
wr (in) - Write trigger signal, must be asserted for the entire transfer
din (in) - 8bit data to be sent to the card
din_valid (in) - Indicates that data is present on din
din_taken (out) - Indicates that the controller has taken the data from din

(*) During intialisation the clock is reduced to 1/128, or about 400kHz.

Lawrence Wilkinson
lawrence@ljw.me.uk
2013-05-02
