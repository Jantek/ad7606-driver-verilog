# ad7606-driver-verilog
AD7606 port
=======
AD7606_ctrl.v
-------
**External signals**</br>
These signals can be used to control the sampling start of the entire module</br>
`clk     `: the main clock of the entire module, it is recommended to use a 50M clock, and the timing of some signals may not meet the requirements of the chip manual if the clock is higher</br>
`rst_n   `: the reset signal of the entire module, low-level complex Bit</br>
`en      `: Control the sampling rate of AD7606, control the start of the sampling process through the enable signal to control the sampling of AD7606</br>
`start   `: start sampling signal, high level means start sampling; at this time, if en is high, start sampling; when the level is low When the AD7606 will not enter the sampling state</br>

**AD7606 control signal**</br>
These ports are directly connected to AD7606, and will produce corresponding changes according to external signals</br>
`busy    `: AD7606’s busy output signal, when all channels (8 channels) start sampling, the signal becomes high, and the signal is pulled down after sampling</br>
`fdata   `: AD7606’s Indication signal, in the sampling result output stage, the signal is pulled high to indicate that the output data is the data of one channel</br>
`cvtData `: AD7606 parallel data output port</br>
`cs      `: AD7606 chip select signal, low level active</br>
`rd      `: AD7606 read signal, low level active</br>
`cvtX    `: AD7606 channel sampling signal, cvtA, cvtB</br>
`range   `: AD7606 analog input voltage range selection, high level is 10V, low level is 5V</br>
`phy_rst `: AD7606 hardware reset signal, high level is valid</br>
`vio     `: AD7606 IO port voltage selection</br>

**Read signal of AD7606**</br>
Reading these data can better control AD7606</br>
`chx     `: channel data read back from AD7606, x has 1-8</br>
`update  `: AD7606 data update indication signal, high means that the data has been updated</br>
`phy_busy`: AD7606 busy status signal, High means the AD7606 is busy</br>

**Constant definition**</br>
`RANGE_10V`: control range , when it is 1, it means that the analog input range is 10V, and when it is 0, it means that the analog input range is 5V:</br>
`WAIT_CNT `: used in the debugging process, reserved</br>
`T2       `: cvtX the number of times to keep the low level, the chip manual cvtX recommends to keep 25ns, so it is used here 2 (40ns) to ensure that the low level time meets the timing requirements</br>

generate_en.v
------
**External signal**</br>
clk : main clock of the whole module</br>
rst_n : reset signal of the whole module, low level reset</br>

**The output signal of AD7606**</br>
en_o : the output enable signal of the module</br>

**Constant definition**</br>
INTERVAL_CNT : the cycle number setting of the enable signal</br>
AD7606Demo</br>
ad_top.v</br>

It is necessary to instantiate a PLL phase-locked loop and name it pll, and add three verilog files to the project, bind the pins and then compile and pass. This Demo collects signals at a sampling rate of 200K and outputs them.</br>

Although the AD7606 module used may be different, the relevant port control and other operations should be similar, because they all use an AD7606 chip</br>

![AD7606](https://raw.githubusercontent.com/maxs-well/ad7606-driver-verilog/master/img/hardware.jpg)<br/>

**Environment**</br>
Quartus II 13.0</br>
Windows 7</br>
