How a pressure wave becomes numbers:

Why 24 bit is more than your ears can use？

Why 5 ms can still ruin a performance

Which three numbers describe every digital audio chain


1. explain why every dB value is a ratio and name the reference of dB SPL, dBu, dBV, dBFS

2. derive the sound pressure level and compute the gain a microphone needs

3. state Nyquist and predict an alias frequency

4. derive DR ≈ 6.02 N + 1.76 dB for N-bit audio

5. calculate buffer time and estimate round-trip latency

# p18
### 1. The Big Idea: What is a Decibel ($\text{dB}$)?
A decibel is **not an absolute measurement** (like meters, grams, or seconds). It is always a **ratio comparing two things**—the signal you have ($P$ or $A$) against a fixed reference point ($P_0$ or $A_0$).
- Think of it like saying _"this object is 5 times heavier than a standard 1 kg weight."_ In $\text{dB}$, we use logarithms to compress very large or very small numbers into a manageable scale.
 
 
 ==🟡**why use decibel?**==
#### 1. The Human Ear Works Logarithmically (Compression)
The human body does not perceive sound linearly; it perceives it logarithmically.
- ==🟡If a sound is $10$ times more powerful, it doesn't sound "ten times louder" to your ears—it only sounds about **twice** as loud.==
- To make a sound feel like it is increasing in loudness at an even, linear pace, you have to multiply the physical power exponentially (e.g., $1\times$, $10\times$, $100\times$, $1,000\times$).
- Decibels turn that awkward multiplication chain ($1, 10, 100, 1000$) into a neat, additive scale ($0\text{ dB}, 10\text{ dB}, 20\text{ dB}, 30\text{ dB}$). Every time you add $10\text{ dB}$, the sound roughly doubles in perceived loudness.

#### 2. Handling Massive Numbers Becomes Easy
In electronics and acoustics, the numbers we deal with span a mind-bogglingly huge range.
- Think about a radio receiver: the tiny antenna signal might be $0.000000001\text{ Watts}$ ($1\text{ nanowatt}$), while the power coming out of the transmitter might be $100,000\text{ Watts}$.
- Trying to multiply, divide, or plot a graph using numbers like $0.000000001$ and $100,000$ is messy and prone to errors.
- Using logarithms compresses that massive span into a friendly range of small, manageable integers (in this case, roughly $-120\text{ dB}$ to $+80\text{ dB}$).

#### 3. Multiplication Turns Into Simple Addition
When a signal passes through a chain of audio or electronic gear (like a microphone $\rightarrow$ cable $\rightarrow$ preamp $\rightarrow$ mixer $\rightarrow$ amplifier), each piece multiplies or divides the signal (e.g., $\times 2$, then $\times 10$, then $\div 4$).
- If you use raw "times," you have to multiply all those fractions and large numbers together at every single stage.
- Because of how logarithms work, **multiplication inside a log becomes addition outside of it**. When you use decibels, you just **add and subtract** the $\text{dB}$ values at each step ($+6\text{ dB} + 20\text{ dB} - 12\text{ dB}$). It makes system design and engineering math infinitely faster and easier.

### 2. Why Are There Two Different Formulas ($10$ vs $20$)?
You will notice two formulas in the image:
- $L = 10 \log_{10} \left(\frac{P}{P_0}\right)$ for **Power**
- $L = 20 \log_{10} \left(\frac{A}{A_0}\right)$ for **Amplitude / Voltage**
**Why the difference of 10 vs 20?** In physics and electronics, **Power is proportional to the square of Voltage/Amplitude** ($P \propto A^2$). $$P = \left(\frac{V}{R}\right) \cdot V = \frac{V^2}{R}$$When you put a squared term inside a logarithm, the exponent comes out front as a multiplier:$$\log_{10}(A^2) = 2 \cdot \log_{10}(A)$$Multiplying that $2$ by the standard power factor of $10$ gives you **$20$** for voltage or amplitude measurements.

### 3. What Do All the Letters Mean?
Because different industries measure signals differently, they set different baseline "zeros" ($A_0$ or $P_0$):
- $\text{dBu}$ ($0.775\text{ V}_{\text{RMS}}$): Used in professional audio gear (like mixing consoles). Where does that weird number $0.775\text{ V}$ come from? It's the voltage required to dissipate $1\text{ milliwatt}$ of power across a standard $600\text{-ohm}$ resistor ($\sqrt{1\text{ mW} \cdot 600\ \Omega} \approx 0.775\text{ V}$)$（P = \left(\frac{V}{R}\right) \cdot V = \frac{V^2}{R}）$.

**dBu is a measurement of voltage**, but it is expressed in decibels relative to a specific reference voltage rather than as a raw volt value.
To break that down:
**The Reference:** The "u" in dBu historically stands for unloaded. The reference voltage ($A_0$) is **$0.775\text{ V}_{\text{RMS}}$**.
**Where it comes from:** That specific number isn't random—it is the voltage needed to produce $1\text{ milliwatt}$ of power across a standard $600\text{-ohm}$ circuit ($\sqrt{1\text{ mW} \cdot 600\ \Omega} \approx 0.775\text{ V}$).
**How it works:** ==🟡When you see a reading in dBu, you are using the voltage formula ($20 \log_{10} \frac{V}{0.775}$) to see how many decibels your signal is above or below that $0.775\text{ V}$ baseline. For example, $0\text{ dBu}$ means your signal is exactly $0.775\text{ V}_{\text{RMS}}$.==

==🟡**Example 1: Doubling the Voltage (+6 dB)**==
- **The Situation:** You turn up a knob or a preamp, and the output voltage doubles from $0.775\text{ V}$ to **$1.55\text{ V}_{\text{RMS}}$**.
- **The Math:**$$\text{dBu} = 20 \log_{10}\left(\frac{1.55}{0.775}\right) = 20 \log_{10}(2)$$Since $\log_{10}(2) \approx 0.301$:$$\text{dBu} \approx 20 \cdot 0.301 \approx +6.02\text{ dBu}$$
- **What it means:** In the decibel world, **doubling a voltage is always a $+6\text{ dB}$ increase** (regardless of what the starting voltage was).

==🟡**Example 2: Professional Audio Standard Operating Level (+4 dBu)**==
- **The Situation:** Professional mixing consoles and studio hardware operate on a standard nominal level known as **$+4\text{ dBu}$**. What does that actually mean in volts?
- **The Math:** We work backward from the formula:$$4 = 20 \log_{10}\left(\frac{V}{0.775}\right)$$
    Divide by 20:$$0.2 = \log_{10}\left(\frac{V}{0.775}\right)$$
    Take $10$ to the power of both sides ($10^{0.2} \approx 1.585$):$$1.585 = \frac{V}{0.775}$$
    Multiply by $0.775$:$$V \approx 1.23\text{ V}_{\text{RMS}}$$
**What it means:** ==🟡When a piece of pro audio gear says it's running at $+4\text{ dBu}$, it means it is pumping out **$1.23\text{ volts}$** of electrical signal under normal operation.==
- $\text{dBV}$ ($1\text{ V}_{\text{RMS}}$): Used in consumer audio (like home stereos or AUX cables). It uses a clean, straightforward reference of exactly $1\text{ volt}$.
- $\text{dB SPL}$ ($20\ \mu\text{Pa}$): Used in acoustics and sound levels. It compares sound pressure against $20\ \mu\text{Pa}$ ($\text{micropascals}$), which is roughly the quietest sound a young human ear can hear (the threshold of hearing).
- $\text{dBFS}$ (**Full-Scale**): Used in digital audio (like your computer, DAWs, or digital files). Here, $0\text{ dB}$ is the **absolute maximum** digital limit before clipping/distortion happens, so all valid measurements are negative numbers (e.g., $-12\text{ dBFS}$).



# p19
![[Pasted image 20261101181341.jpg]]
audio analog meter


VU PPM LUFS SPL are just different types of Audio meters.



==🟡**Why Audio meter needs time constant?**==
We need a **time constant** (or time behavior) in audio meters for two major reasons: **human biology** and **readability**.
Without a time constant, meters would either be completely unreadable or fail to show you what your ears are actually experiencing. Here is why they are essential:
### 1. To Match How Human Ears and Brains Work
Physical sound waves hit the eardrum instantly, but human perception doesn't work that way. The human ear-brain system acts like an integrator—it takes a small window of time to accumulate acoustic energy before we actually register how "loud" a sound is.
- If a meter reacted with absolute, mathematical instantaneity, it would measure raw physical phenomena rather than human-perceived loudness.
- By building a time constant into the meter (like the $\approx 300\text{ ms}$ delay on a VU meter or the $400\text{ ms}$ window on a LUFS meter), the tool mimics real human listening.
### 2. To Make the Display Readable (Preventing "Jitter")
Audio signals are full of lightning-fast spikes, micro-transients, and high-frequency variations that happen thousands of times a second.
- If a physical needle or digital display had zero delay, it would vibrate, flicker, and bounce around so erratically that it would become a complete blur.
- A time constant smooths out these hyper-fast fluctuations, giving the needle or display a stable, readable movement so an engineer can actually interpret the level.

==🟡**How time constant works? which kind of time constant do you mean? like latency in online game？**==
No, it is **not like latency** (lag) in an online game.
In a video game, latency is a _delay_—the time it takes for your button-press data to travel across the internet to a server and back.
An audio meter's **time constant** is something entirely different: it is a **smoothing or averaging window** (essentially a low-pass filter or mechanical damping) that dictates _how long_ the meter takes to react to and release from a signal change.
### How a Time Constant Works (The Engineering View)
At its core, a time constant determines how a system responds to changes over time:
1. **In Analog Circuits (RC Circuits):** A traditional VU meter uses a resistor and a capacitor ($\text{RC}$). When an audio signal comes in, it charges the capacitor. Just like filling a bucket with a small hole in it, the voltage builds up gradually and drains away gradually. The time constant ($\tau = R \times C$) defines that exact charging and discharging speed.
    
2. **In Digital/Software Meters:** It is written as a mathematical moving-average or exponential smoothing filter in code, telling the software: _"Don't show me every single sample; instead, calculate the rolling energy over a specific window of time."_
### Why Different Meters Use Different Time Constants
Because different audio tasks require different views of the sound, engineers design meters with asymmetric or varied time behaviors:
- The VU Meter ($\approx 300\text{ ms}$): Its time constant is symmetric and relatively slow ($\approx 300\text{ ms}$ rise and fall). This acts like a heavy mechanical damper, ensuring the needle ignores rapid micro-transients and only displays the smooth, averaged energy of the music.
    
- The PPM Meter ($10\text{ ms}$ attack, $1.5\text{ s}$ decay): This uses an **asymmetric** time constant.
    - Its **attack** is blazing fast ($10\text{ ms}$) so the needle flies up _instantly_ the moment a sharp peak (like a snare drum) hits.
    - Its **decay** is very slow ($1.5\text{ s}$) so that the peak lingers on the screen long enough for human eyes to actually read it before it drops back down.

| **Meter Type** | **Full Name**             | **Domain**                    | **What It Measures**                                                                          | **Typical Time Constant / Window**                                  |
| -------------- | ------------------------- | ----------------------------- | --------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| **VU**         | Volume Unit               | Electrical (Analog)           | Average signal energy, designed to mimic human hearing inertia.                               | $\approx 300\text{ ms}$ (symmetric rise and fall)                   |
| **PPM**        | Peak Programme Meter      | Electrical (Analog / Digital) | Rapid transient peaks to prevent signal overload and distortion.                              | Fast $10\text{ ms}$ attack / slow $1.5\text{ s}$ decay              |
| **LUFS**       | Loudness Units Full Scale | Digital (Software / DAWs)     | Perceived human loudness over time for streaming and broadcast compliance.                    | $400\text{ ms}$ (short-term) to multi-second integrated windows     |
| **SPL**        | Sound Pressure Level      | Acoustic (Air Pressure)       | Physical sound pressure waves in a real-world environment (referenced to $20\ \mu\text{Pa}$). | Fast ($\approx 125\text{ ms}$) or Slow ($\approx 1\text{ s}$) modes |
### 1. VU (Volume Unit)
- **What it is:** A traditional analog measurement standard designed to show average signal energy, closely mirroring the natural inertia of human hearing.
- **Where it is used:** On analog mixing consoles, outboard vintage hardware equipment, and retro audio gear plugins.
- **How it works:** It uses a relatively slow, symmetric time constant (≈300 ms\approx 300\text{ ms}≈300 ms rise and fall time) calibrated to a standard baseline of 0 VU=+4 dBu0\text{ VU} = +4\text{ dBu}0 VU=+4 dBu (1.23 VRMS1.23\text{ V}_{\text{RMS}}1.23 VRMS​).
- **Main Purpose:** To track sustained signal levels, monitor overall musical body, and establish gain staging across analog equipment without reacting erratically to fast volume spikes.

### 2. PPM (Peak Programme Meter)
- **What it is:** A specialized peak-detection measurement standard designed to capture rapid transient volume spikes rather than average energy.
- **Where it is used:** In radio and TV broadcast facilities, master control rooms, and analog magnetic tape recording setups.
- **How it works:** It utilizes an asymmetric time constant with an ultra-fast 10 ms10\text{ ms}10 ms attack time to register instantaneous signal spikes instantly, paired with a slow 1.5 s1.5\text{ s}1.5 s decay time to hold the reading long enough for human visual inspection.
- **Main Purpose:** To prevent signal clipping, protect transmission equipment from overload distortion, and ensure peak headroom limits are strictly maintained.

### 3. LUFS (Loudness Units Full Scale)
- **What it is:** A modern digital loudness measurement standard designed to match how the human brain perceives volume over time (based on EBU R128 and BS.1770 specifications).
- **Where it is used:** Inside computers, Digital Audio Workstations (DAWs), streaming services (like Spotify and YouTube), and television broadcast systems.
- **How it works:** It applies sophisticated frequency weighting and standardized time constants (such as $400\text{ ms}$ short-term windows and multi-second integrated averages) to evaluate the perceived loudness of an audio file.
- **Main Purpose:** To normalize playback volumes across different platforms so listeners don't have to constantly adjust their volume knobs when switching between tracks.

### 4. SPL (Sound Pressure Level)
- **What it is:** A physical acoustic measurement standard used to quantify real-world air pressure variations caused by sound waves.
- **Where it is used:** At live concert venues, recording studio control rooms, industrial workplaces, and acoustic research laboratories.
- **How it works:** It uses an acoustic microphone capsule calibrated against the human hearing threshold $(20 μPa=0 dB\ SPL )$, combining frequency weighting (such as A-weighting for human sensitivity) with Fast $(≈125 ms)$ or Slow $(≈1 s)$ time integration modes.
- **Main Purpose:** To evaluate real-world acoustic volume in a room, enforce local noise pollution laws, and protect human ears from hearing damage.



# p20
- **$I$ (Sound Intensity):** The amount of acoustic power flowing through a given area, measured in watts per square meter ($\text{W/m}^2$).
- **$p$ (RMS Sound Pressure):** The root-mean-square pressure fluctuation caused by the sound wave, measured in Pascals ($\text{Pa}$). It is squared ($p^2$) because energy is proportional to the square of a wave's amplitude.
- **$\rho$ (Density of the Medium):** The density of the fluid (e.g., air), measured in $\text{kg/m}^3$. At standard sea-level conditions, air density is roughly $1.2\text{ kg/m}^3$.
- **$c$ (Speed of Sound):** How fast sound travels through the medium, measured in meters per second ($\text{m/s}$). In room-temperature air, this is roughly $343\text{ m/s}$.
### The Acoustic Impedance ($\rho c$)
The product **$\rho c$** is known as the **characteristic acoustic impedance** of the medium.
- Think of $\rho c$ as how "resistant" or "stubborn" the air is to being compressed and displaced by sound waves.
- **The Electrical Analogy:** This is very similar to Ohm's Law for electrical power ($P = \frac{V^2}{R}$), where voltage corresponds to sound pressure ($p$), and electrical resistance ($R$) corresponds to acoustic impedance ($\rho c$).

Here is how the math works step-by-step:
1. **Power vs. Amplitude:** Decibels are fundamentally defined around **power or intensity** ($I$), which uses a factor of 10:$$L = 10 \log_{10} \frac{I}{I_0}$$
2. **The Acoustic Relationship:** In physics, acoustic intensity ($I$) is proportional to the square of the sound pressure ($p^2$), expressed as $I = \frac{p^2}{\rho c}$.
3. **The Logarithm Rule:** When you substitute $p^2$ into the intensity equation, you get:$$L_p = 10 \log_{10} \frac{p^2}{p_0^2}$$
Using the logarithm power rule ($\log(x^2) = 2 \log(x)$), the exponent **$2$ comes down and multiplies the $10$**, turning it into **$20$**:$$L_p = 20 \log_{10} \frac{p}{p_0} \text{ dB}$$
4. **The Reference ($p_0$):** The baseline reference pressure is set to **$20\ \mu\text{Pa}$**, which represents the ==🟡standard threshold of human hearing at $1\text{ kHz}$==.


**==🟡Standard threshold of human hearing at $1\text{ kHz}$==**:
The reference sound pressure level $p_0 = 20\ \mu\text{Pa}$ (or $2 \times 10^{-5}\text{ Pa}$) was chosen because it represents the **absolute threshold of human hearing for a $1\text{ kHz}$ sine wave** in a healthy young adult.

Here is why $1\text{ kHz}$ is used as the standard benchmark:
- **Human Ear Sensitivity:** The human ear does not hear all frequencies equally well. We are most sensitive to mid-range frequencies between roughly $1\text{ kHz}$ and $4\text{ kHz}$ (the frequency range where human speech and a baby's cry naturally sit).
- **The Benchmark Point:** At $1\text{ kHz}$, the minimum sound pressure required for a typical listener to barely detect a tone in an otherwise silent environment is approximately $20\ \mu\text{Pa}$.
- **Zero Decibels ($0\text{ dB SPL}$):** Plugging $p = 20\ \mu\text{Pa}$ into the SPL formula yields:$$L_p = 20 \log_{10} \left(\frac{20\ \mu\text{Pa}}{20\ \mu\text{Pa}}\right) = 20 \log_{10}(1) = 0\text{ dB SPL}$$Thus, ==🟡$0\text{ dB SPL}$ does not mean "zero sound energy" or "total physical silence"; it simply means the sound pressure is at the average baseline threshold of human audibility at $1\text{ kHz}$.== Sounds quieter than $20\ \mu\text{Pa}$ yield negative dB SPL values (e.g., in ultra-quiet anechoic chambers).


# p21
As sound pressure increases exponentially, decibels give us a manageable logarithmic scale to talk about it:
- **$20\ \mu\text{Pa} = 0\text{ dB}$**: The quietest sound a healthy human ear can hear (threshold of hearing).
- **$2\text{ mPa} = 40\text{ dB}$**: A quiet room or a quiet library.
- **$20\text{ mPa} = 60\text{ dB}$**: Normal human conversation.
- **$1\text{ Pa} \approx 94\text{ dB}$**: An acoustic calibrator (a tool used to test SPL meters).
- **$20\text{ Pa} = 120\text{ dB}$**: A rock concert right near the speakers (the threshold of discomfort).
- **$200\text{ Pa} = 140\text{ dB}$**: The threshold of **pain and physical damage** to the ear (like a jet engine taking off close by).

# p22
Dynamic Condenser Ribbon Piezo refers to different types of microphones

**Dynamic Microphone**: In a dynamic microphone, sound waves push against a lightweight **diaphragm**, which is attached to a small **coil** of wire wrapped around a cylinder. As the sound waves move the diaphragm, the coil moves back and forth inside a permanent **magnet**, generating an electrical current via electromagnetic induction.
![[Pasted image 20261101222443.png]]

![[Pasted image 20261101224326.jpg|336]]
coil
This is a close-up of a physical **voice coil** used in loudspeakers and dynamic microphones. It consists of fine copper wire wound tightly into a cylinder, which fits directly inside a magnetic gap to translate between motion and electricity.


**Condenser Microphone**:A condenser microphone functions as an electrostatic capacitor. It features a ultra-thin conductive **diaphragm** placed very close to a fixed metal **backplate**. When sound waves hit the diaphragm, it flexes closer to or further from the backplate, changing the capacitance and generating an electrical voltage variation using an external bias voltage (like $+48\text{ V}$ phantom power).
![[Pasted image 20261101222450.png|462]]
**Ribbon Microphone**: A ribbon microphone is a specialized type of electromagnetic microphone. Instead of a coil, it suspends an extremely thin, corrugated strip of **metal ribbon** directly between the poles of a strong **magnet**. When sound waves vibrate the lightweight metal ribbon, it cuts through the magnetic field, inducing an electrical audio signal directly from the ribbon.

**Piezoelectric (Crystal) Microphone**:A piezo microphone relies on mechanical stress. Sound waves strike a protective grille and **diaphragm**, which is physically linked to a **piezoelectric crystal (bimorph element)**. When the physical movement bends or stresses the crystal structure, it forces internal electrical charges to shift, creating a voltage output.
![[Pasted image 20261101222832.jpg]]




**Balanced Lines and Noise Cancellation**

**balanced audio cable**: a specialized type of cable designed to eliminate unwanted electrical interference (like hum, buzz, and radio frequency noise) over long cable runs.

**balanced audio cable and balanced line**:
**balanced line** refers to the overall **circuit architecture**, while a **balanced audio cable** is the physical hardware wire used to connect those balanced circuits together.

### How Balanced Lines Work
[How do balanced cables work? Balanced vs unbalanced audio explained](https://www.youtube.com/watch?v=UQPJYWA5Y-o)
A standard balanced cable (such as an XLR cable) uses **three internal conductors** instead of two:
1. **Hot ($+s+n$):** Carries the audio signal in standard polarity, plus any environmental noise ($n$) picked up along the way.
2. **Cold ($-s+n$):** Carries an exact copy of the audio signal with its phase inverted (flipped), plus the same environmental noise.
3. **Ground/Shield:** Shields the inner conductors from outside electromagnetic interference.
At the receiving end, equipment uses a **difference amplifier** to process the signals:$$(+s + n) - (-s + n) = \mathbf{2s}$$**The Result:** Because the noise ($n$) is identical on both signal wires, subtracting them causes the noise to **completely cancel out**. Meanwhile, flipping the phase of the cold signal causes the actual audio signal ($s$) to add together, doubling its strength ($2s$).


# p23
### 1. The Physical Process (The 3 Steps on the Right)
1. **Sound pressure moves the diaphragm:** Acoustic waves ($p(t)$) hit the physical diaphragm, causing it to vibrate back and forth with a velocity $v(t)$.
2. **The attached coil moves in the magnet's field $B$:** Because the voice coil is mechanically linked to the diaphragm, it moves synchronously through the magnetic flux lines produced by the permanent magnet.
3. **Induced voltage is proportional to velocity ($u(t) \propto v(t)$):** As the wire cuts through the magnetic field, Faraday's law of induction generates an output voltage $u(t)$ that directly mirrors the speed of the moving coil.
### 2. The Induction Equation
$$\mathbf{u(t) = B l v(t)}$$
- **$u(t)$**: The induced output voltage over time (the electrical audio signal sent down the cable).
- **$B$**: The strength of the magnetic field (measured in Teslas) created by the permanent magnet.
- **$l$**: The total length of the wire wound inside the voice coil. (A longer wire cuts more magnetic lines, yielding a stronger signal).
- **$v(t)$**: The instantaneous velocity of the diaphragm and coil.
### 3. Practical Characteristics at the Bottom
- **No power needed, robust:** Because it relies entirely on physical motion and permanent magnetism, it requires no external batteries or phantom power, and it can handle extremely high sound pressure levels without breaking.
- **Low sensitivity (a few $\text{mV/Pa}$):** Because the mass of the coil and diaphragm requires physical force to move, they are less sensitive than condenser mics, meaning they typically require **more preamp(preamplifier) gain** from your audio interface to reach a usable level.




# p24
Left Side: Calculating Voltage and Preamp Gain
- **Microphone Sensitivity ($S$):**
    - Sensitivity is measured in $\text{mV/Pa}$ (millivolts per Pascal).
    - As we saw earlier, $94\text{ dB SPL}$ equals a physical pressure of $1\text{ Pa}$. 
     **TheSPL Reference ($p_0$):** Human hearing baseline is set at $20\ \mu\text{Pa}$ ($0.00002\text{ Pa}$).
     **The Formula:** SPL uses a logarithmic scale: $20 \log_{10}(p / p_0)$.
     **The Math:** When you plug in $1\text{ Pa}$ for $p$, you get $20 \log_{10}(1 / 0.00002)$, which equals $20 \log_{10}(50,000)$.
     **The Result:** $\log_{10}(50,000)$ is roughly $4.7$, and $20 \times 4.7$ gives you approximately **$94\text{ dB SPL}$**.Therefore, if a microphone receives $94\text{ dB SPL}$, its output voltage $u$ will directly equal its sensitivity rating $S$.
    
- **Converting Sensitivity to dBV ($S = 10\text{ mV/Pa}$):**
    - A sensitivity of $10\text{ mV/Pa}$ means $0.01\text{ V}$ is produced per Pascal.
    - Expressed in decibels relative to $1\text{ V}$ ($\text{dBV}$):$$20 \log_{10} \left(\frac{0.010\text{ V}}{1\text{ V}}\right) = -40\text{ dBV}$$
- **Calculating Required Preamp Gain ($G$):**
    - Professional studio equipment operates at a standard **line level** of **$+4\text{ dBu}$**, which equals **$1.228\text{ V}$**.
    - If a standard acoustic source produces $94\text{ dB SPL}$ ($1\text{ Pa}$), the microphone outputs only $0.010\text{ V}$. To boost that tiny signal up to professional line level ($1.228\text{ V}$), the preamp must apply a gain ($G$):$$G = 20 \log_{10} \left(\frac{1.228\text{ V}}{0.010\text{ V}}\right) = \mathbf{41.8\text{ dB}}$$
    - The preamp needs to add roughly $42\text{ dB}$ of gain just to bring a normal conversation-level sound up to standard studio operating levels!
- **Handling a Loud Source ($120\text{ dB SPL}$):**
    - If a much louder sound hits the mic ($120\text{ dB SPL} = 20\text{ Pa}$), the output voltage scales up linearly:$$20\text{ Pa} \times 10\text{ mV/Pa} = 200\text{ mV} = \mathbf{0.2\text{ V}}$$

dBV 和 dBu?
dBV（以 1 伏特为基准）
     **基准电压**：$1\text{ V}$（即 $0\text{ dBV} = 1\text{ V}$）
     **计算公式**：$$\text{dBV} = 20 \log_{10}\left(\frac{V}{1\text{ V}}\right)$$**应用场景**：常用于消费级音频设备（如民用耳机、RCA莲花接口设备、便携录音机等）。
     **特点**：简单直观，以 $1\text{ V}$ 作为绝对门槛。例如，输出电压为 $1\text{ V}$ 的设备其电平就是 $0\text{ dBV}$。

dBu（以 0.775 伏特为基准）
     **基准电压**：$0.775\text{ V}$（即 $0\text{ dBu} = 0.775\text{ V}$）。_(注：历史原因源于早期电话电路的标准，即在 $600\ \Omega$ 负载下产生 $1\text{ mW}$ 功率所需的电压：$U = \sqrt{P \times R} = \sqrt{0.001\text{ W} \times 600\ \Omega} \approx 0.775\text{ V}$)_。
     **计算公式**：$$\text{dBu} = 20 \log_{10}\left(\frac{V}{0.775\text{ V}}\right)$$**应用场景**：广泛用于专业音频领域（如调音台、专业音频接口、话放输出等）。前面幻灯片中提到的专业标准工作电平 **$+4\text{ dBu}$** 就是基于此单位（折算下来约为 $1.228\text{ V}$）。
    - The preamp needs to add roughly $42\text{ dB}$ of gain just to bring a normal conversation-level sound up to standard studio operating levels!
    **Handling a Loud Source ($120\text{ dB SPL}$):**
    - If a much louder sound hits the mic ($120\text{ dB SPL} = 20\text{ Pa}$), the output voltage scales up linearly:$$20\text{ Pa} \times 10\text{ mV/Pa} = 200\text{ mV} = \mathbf{0.2\text{ V}}$$

# p25
### 1. 四种主要的指向性图形

- **Omni（全指向 / 无指向）**
    - **图形**：呈完美的圆形。
    - **特性**：对来自所有方向（前、后、左、右）的声音具有相同的灵敏度。
    - **应用**：常用于声学测量（measurement）或需要捕捉完整环境音的场景。
        
- **Cardioid（心形指向）**
    - **图形**：呈心形，正面灵敏度最高，正后方声音会被极大衰减。
    - **特性**：能够有效拒绝来自后方的声音，防止舞台上的回授（feedback）。
    - **应用**：广泛用于现场舞台表演、人声录音等。
        
- **Hypercardioid（超心形指向）**
    - **图形**：比心形指向更窄，正面的拾音范围更集中，但在正后方会产生一个小型的“尾瓣”（rear lobe）。
    - **特性**：侧面抑制能力极强，但需要注意后方的微弱拾音。
        
- **Figure-8（8字形 / 双指向）**
    - **图形**：呈对称的两个环，像数字“8”。
    - **特性**：对正前方和正后方的声音敏感，但会完全阻隔来自正侧方的声音（侧面抑制能力极佳）。
    - **应用**：常用于铝带麦克风（ribbon）以及 M/S（Mid-Side）立体声拾音技术。

### 2. 数学公式与混合模型
图片中间给出了一个统一的数学表达式，用来描述这些指向性的极坐标方程：
$$r(\theta) = a + (1-a)\cos\theta$$
其中参数 $a$ 的取值决定了麦克风的指向类型（对应取值 $1, 0.5, 0.25, 0$）：
- 当 **$a = 1$** 时：$r(\theta) = 1$，即全指向（Omni）。
- 当 **$a = 0.5$** 时：呈现标准的心形指向（Cardioid）。
- 当 **$a = 0$** 时：$r(\theta) = \cos\theta$，即8字形指向（Figure-8）。


# p26
### 1. Sample Rate ($f_s$)
- **What it is:** The number of times per second an analog-to-digital converter (ADC) samples the continuous audio voltage waveform.
- **Core Impact:** Determines the allowable audio **bandwidth**.
- **Key Principle:** According to the Nyquist theorem, the maximum frequency a system can accurately capture without aliasing is strictly less than half the sample rate ($\text{bandwidth} < f_s / 2$). For example, standard CD audio ($44.1\text{ kHz}$) covers frequencies up to $\approx 22.05\text{ kHz}$.

### 2. Bit Depth ($N$)
- **What it is:** The number of binary bits allocated to store the amplitude of each individual audio sample (e.g., 16-bit, 24-bit).
- **Core Impact:** Determines the available **dynamic range**.
- **Key Principle:** A higher bit depth provides finer vertical resolution (quantization steps), lower quantization noise, and a wider range between the quietest and loudest clean signals (roughly $6\text{ dB}$ of dynamic range per bit).

### 3. Buffer Size ($B$)
- **What it is:** The number of audio samples accumulated in memory before the host system (CPU/DAW) processes the block.
- **Core Impact:** Determines system **latency** (delay).
- **Key Trade-off:**
    - **Small Buffer (e.g., 64 or 128 samples):** Reduces processing delay for low-latency real-time monitoring during recording, but increases CPU load and risk of audio dropouts.
    - **Large Buffer (e.g., 512 or 1024 samples):** Gives the CPU more processing time for complex mixing plugins, but introduces noticeable latency.




# p27

### 1. Nyquist Sampling Theorem
- **Formula:** $f_s > 2 f_{\text{max}}$
- **Core Concept:** To perfectly reconstruct an analog signal without distortion, the sampling rate $f_s$ must be strictly greater than twice the highest frequency component ($f_{\text{max}}$) present in the signal.

### 2. What is Aliasing?
- **Visual Breakdown:** The black dots represent the discrete sample points taken at a sample rate of **$f_s = 8\text{ kHz}$** (a sampling interval of $0.125\text{ ms}$).
- **The Problem:** The solid brown curve represents a **$5\text{ kHz}$** high-frequency sine wave, while the dashed green curve represents a **$3\text{ kHz}$** lower-frequency sine wave. Because the sampling rate is too low ($8\text{ kHz} < 2 \times 5\text{ kHz}$), both completely different frequencies intersect at the exact same sampling dots!
- **The Result:** The system misinterprets the high-frequency $5\text{ kHz}$ tone as a false $3\text{ kHz}$ tone. Once aliased into the digital domain, this distortion cannot be filtered out.
- **Alias Frequency Formula:** $f_a = \vert{}f - k f_s\vert{}$ (where $k$ is an integer). In this example, $f_a = \vert{}5\text{ kHz} - (1 \times 8\text{ kHz})\vert{} = \mathbf{3\text{ kHz}}$.

### 3. Practical Solutions
- **Anti-Aliasing Low-Pass Filter:** An analog low-pass filter must be placed **before** the Analog-to-Digital Converter (ADC) to remove any frequencies higher than $f_s / 2$, preventing them from folding back into the audible band.
- **Why CD Audio uses $44.1\text{ kHz}$:**
   Step 1: The Human Hearing Limit ($20\text{ kHz}$)
- Human hearing generally tops out at around **$20\text{ kHz}$** (and often less as we age).
- According to the Nyquist theorem ($f_s > 2f_{\text{max}}$), to capture up to $20\text{ kHz}$, your sampling rate needs to be greater than $2 \times 20\text{ kHz} = \mathbf{40\text{ kHz}}$.
- So, theoretically, any sampling rate above $40\text{ kHz}$ (like $40\text{ kHz}$ flat) would cover all audible frequencies. **So why not use $40\text{ kHz}$?**

   Step 2: The Problem with Real Filters (The "Transition Band")
To prevent aliasing, you need an **anti-aliasing low-pass filter** _before_ the ADC to chop off everything above half your sampling rate.
- **Ideal Filter (Impossible):** An ideal filter would act like a vertical cliff—letting $20\text{ kHz}$ pass completely untouched, and instantly blocking $20.0001\text{ kHz}$.
- **Real Filter (Sloped):** Real-world analog electronic filters cannot drop off like a cliff. They have a **slope** (transition band). They take some physical frequency distance to roll off from "letting sound through" to "blocking sound completely."
If your sampling rate was exactly $40\text{ kHz}$, half of it is $20\text{ kHz}$. That means your filter would have to start rolling off _before_ $20\text{ kHz}$, which would permanently cut off the highest frequencies you actually want to hear!
![[Pasted image 20261102005144.png]]
low pass filter

Step 3: Why $44.1\text{ kHz}$ Solves This
By bumping the sampling rate up from $40\text{ kHz}$ to **$44.1\text{ kHz}$**:
- Half of $44.1\text{ kHz}$ is **$22.05\text{ kHz}$**.
- This gives you a safe buffer zone (a **transition band**) from $20\text{ kHz}$ to $22.05\text{ kHz}$.
- Your analog filter has plenty of "room" to gently roll off and block all unwanted frequencies above $22.05\text{ kHz}$ _without_ ever touching or distorting the high-end frequencies up to $20\text{ kHz}$ that humans can hear.
![[{78FC5F1D-1A40-4666-A87F-AB8EA5A04742}.png]]





















