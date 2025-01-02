# Alarm-Clock-VL
### Verilog Clock with Alarm Functionality

This Verilog design generates a 24-hour format clock with seven output signals, including `Alarm`, `Hour`, `Minute`, and `Seconds`. The clock allows for initial time configuration, alarm setup, and supports reset and alarm management functionalities. Below are the details of its functionality and signals:

---

#### Clock Features:

1. 24-Hour Format: The clock operates in a 24-hour format.
2. Initial Time Setup: The initial time can be set when `reset` is high or when `LD_time` is set to 1.
3. Alarm Configuration: Alarm time is configured using `LD_alarm`, and it activates only if `AL_ON` is high.
4. Alarm Control: The alarm signal can be stopped by activating `STOP_al`.
5. Clock Signal Generation: A 1-second clock is derived from a 10Hz input clock to update seconds, minutes, and hours accordingly.

---

#### Input Signals:

1. `reset`:  
   - Active-high signal to reset the system.  
   - Sets the clock to the provided input hour and minute (`H_in1`, `H_in0`, `M_in1`, `M_in0`), and seconds to `00`.  
   - Resets alarm time to `00:00:00` and deactivates `Alarm`.  
   - For normal operation, this signal should be low.

2. `clk`:  
   - 10Hz input clock signal, used to generate the 1-second clock.

3. `H_in1`, `H_in0`, `M_in1`, `M_in0`:  
   - Inputs to configure the clock or alarm:  
     - `H_in1` (2-bit): Most significant hour digit (0-2).  
     - `H_in0` (4-bit): Least significant hour digit (0-9).  
     - `M_in1` (4-bit): Most significant minute digit (0-5).  
     - `M_in0` (4-bit): Least significant minute digit (0-9).  

4. `LD_time`:  
   - When high, the clock time is set to the provided inputs (`H_in1`, `H_in0`, `M_in1`, `M_in0`) and seconds to `00`.  
   - When low, the clock operates normally, updating seconds every 10 clock cycles.

5. `LD_alarm`:
   - When high, the alarm time is set using the provided inputs (`H_in1`, `H_in0`, `M_in1`, `M_in0`).  
   - When low, the clock operates normally.

6. `STOP_al`:  
   - Brings the `Alarm` output low when it is high.

7. `AL_ON`:
   - Activates the alarm function when high. The alarm rings if the alarm time matches the current clock time.  
   - If low, the alarm function is disabled.

---

#### **Output Signals:**

1. **`Alarm`:**  
   - Goes high if the current time matches the alarm time and `AL_ON` is high.  
   - Remains high until `STOP_al` is activated, which resets it.

2. **Clock Digits:**  
   - `H_out1`: Most significant hour digit (0-2).  
   - `H_out0`: Least significant hour digit (0-9).  
   - `M_out1`: Most significant minute digit (0-5).  
   - `M_out0`: Least significant minute digit (0-9).  
   - `S_out1`: Most significant second digit (0-5).  
   - `S_out0`: Least significant second digit (0-9).

---

#### Internal Signals:

1. Clock Generation:  
   - `clk_1s`: 1-second clock signal.  
   - `tmp_1s`: Counter for generating the 1-second clock.

2. Time Counters:  
   - `tmp_hour`, `tmp_minute`, `tmp_second`: Temporary counters for hours, minutes, and seconds.

3. Current and Alarm Values:  
   - `c_hour1`, `a_hour1`: Most significant hour digits for the clock and alarm.  
   - `c_hour0`, `a_hour0`: Least significant hour digits for the clock and alarm.  
   - `c_min1`, `a_min1`: Most significant minute digits for the clock and alarm.  
   - `c_min0`, `a_min0`: Least significant minute digits for the clock and alarm.  
   - `c_sec1`, `a_sec1`: Most significant second digits for the clock and alarm.  
   - `c_sec0`, `a_sec0`: Least significant second digits for the clock and alarm.  
---
This design ensures proper timekeeping, alarm functionality, and easy configuration for various use cases
