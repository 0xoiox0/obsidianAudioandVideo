![[Pasted image 20261103153848.png]]
### 1. The Three Domains
- **Air (Acoustics)**: Measures sound pressure ($p$) in Pascals ($\text{Pa}$) using **$\text{dB SPL}$**.
    - **Reference**: $20\,\mu\text{Pa}$ (the standard threshold of human hearing).
- **Wire (Analogue)**: Measures electric voltage ($U$) in Volts ($\text{V}$) using **$\text{dBu}$** or **$\text{dBV}$**.
    - **Reference**: $0.775\,\text{V}$ (for $\text{dBu}$) or $1.0\,\text{V}$ (for $\text{dBV}$).
- **Numbers (Digital)**: Measures quantization levels across $N$ bits using **$\text{dBFS}$** (Decibels relative to Full Scale).
    - **Reference**: Full scale (0 dBFS, the maximum digital limit before clipping).
### 2. Signal Conversion Flow
- **Microphone**: Converts mechanical pressure in the air into analogue voltage in a wire ($\text{Air} \rightarrow \text{Wire}$).
- **A/D Converter**: Converts analogue voltage into digital sample numbers ($\text{Wire} \rightarrow \text{Numbers}$).
- **D/A Converter & Loudspeaker**: Reverses the chain, turning digital numbers back into voltage and then physical air displacement.



# p7
![[Pasted image 20261103155328.png]]
**wavelength determine the frequency**
They are bound together by the fundamental wave equation:
$$\text{Speed} = \text{Frequency} \times \text{Wavelength}$$
$$v = f \cdot \lambda$$
Here is how it works in practice:
- **The Speed of Sound is Constant:** In air at room temperature, sound always travels at a constant speed of roughly $343\text{ m/s}$.
- **The Inverse Relationship:** Because speed ($v$) is fixed, if you change the **frequency** ($f$), the **wavelength** ($\lambda$) must change inversely to keep the equation balanced ($f = \frac{v}{\lambda}$).
    - **High frequency** = Short wavelength (waves pack closely together).
    - **Low frequency** = Long wavelength (waves spread far apart).
### Example from the Image
Looking at the interactive graphic from the source:
- At a tone of **$551\text{ Hz}$**, the wavelength in air is **$62\text{ cm}$** ($0.62\text{ m}$).
- If you multiply them: $551\text{ Hz} \times 0.62\text{ m} \approx 341.6\text{ m/s}$, which is the speed of sound in air.

**Core Principle**: A sound wave has a **length**, and objects have a **size**. The interaction between the two determines what the sound does when it encounters an obstacle.
- **Longer Waves (Compared to Object Size)**: When the wavelength is much larger than the object (e.g., a $551\text{ Hz}$ tone with a $62\text{ cm}$ wavelength encountering a $2.5\text{ cm}$ coin), the sound wave simply **flows around it**.
- **Similar Size (Wavelength $\approx$ Object Size)**: When an object is comparable in scale to the wavelength (e.g., a $20\text{ cm}$ head or loudspeaker interacting with the sound wave), it causes **reflections and resonance**.
- **Shorter Waves (Compared to Object Size)**: When the wavelength is much smaller than the physical barrier (e.g., a $5\text{ m}$ wall), the sound wave is **blocked or beamed**.


==🔵Treble:高音==
==🔴Long waves bend around small things.==
- **Size Comparison:** When a sound wave's wavelength is much larger than the physical object in its path, the wave doesn't "see" the object as a solid barrier. Instead, the pressure front passes the obstacle and wraps around the other side.
- **Real-World Example (Bass in a Room):** Low-frequency bass notes have wavelengths ranging from roughly $1.7\text{ meters}$ to $17\text{ meters}$. Because these waves are massive compared to everyday objects like furniture, walls, or pillars, they bend around them effortlessly. This is why you can hear the deep "thump" of a bass guitar or subwoofer even if you are standing behind a wall or in another room—the bass fills the entire space.

==🔴Short waves are blocked or sent in one direction.==
High-frequency treble sounds have very short wavelengths—ranging from about $1.7\text{ cm}$ up to $8.5\text{ cm}$.
- When a wave encounters an object that is larger than its wavelength (like a wall, a piece of furniture, or even your own head), the wave **cannot bend around it** (diffraction is minimal).
- Instead, the obstacle acts as a physical barrier. The sound wave is either reflected back or absorbed, creating a distinct **acoustic shadow** behind the object where those high frequencies simply don't reach.



==🔴A membrane, a wall or a circuit has mass and springiness. It follows slow changes, but not fast ones, or it rings at its own favourite frequency.==
==🔵membrane==
![[Pasted image 20261103161233.jpg]]
### How It Relates to Mass and Springiness
Think about how a speaker cone is built:
- **The Membrane (Cone/Dome):** Usually made of paper, plastic, or lightweight metal, it has physical **mass**. To move it back and forth thousands of times a second, the voice coil and magnet have to push and pull that mass.
- **The Suspension (Surround & Spider):** The flexible ring around the edge of the speaker cone and the accordion-like part inside act like a spring. They give the membrane its **springiness**, providing restoring force to pull the cone back to its resting center position.


==🔴Every device has a different **gain** at every frequency. That is the **frequency response**.==
Every audio device—whether it's a microphone, a pair of headphones, a guitar amplifier, or a room speaker—behaves differently depending on the frequency of the sound passing through it.
- **What is "Gain"?** In this context, gain refers to how much the device amplifies or reduces a signal. A gain of $0\text{ dB}$ means the signal passes through unchanged; positive gain means it is boosted; negative gain (attenuation) means it is quieted down.
- **The "At Every Frequency" Part:** Because of physical limitations like mass, springiness, and cabinet size, a device will naturally be louder at some frequencies and quieter at others.
    - For example, a tiny smartphone speaker might have plenty of gain in the mid-range (so voices sound clear) but very little gain in the bass frequencies (because it lacks the physical size to move enough air).



# p9




# p10
![[Pasted image 20261103163241.png]]
## Sound Pressure Level (SPL)
Sound pressure ($p$) is calculated using the baseline threshold of hearing ($20\text{ }\mu\text{Pa}$) scaled by the decibel level ($L$) via the formula:$$p = 20\text{ }\mu\text{Pa} \cdot 10^{(L/20)}$$





# p11
![[Pasted image 20261103164806.png]]
### 1. Calculate Sound Pressure ($p$) from SPL
The input sound level is $L = 60\text{ dB SPL}$. Using the SPL formula:$$p = 20\text{ }\mu\text{Pa} \cdot 10^{(L / 20)}$$$$p = 20 \times 10^{-6}\text{ Pa} \cdot 10^{(60 / 20)}$$$$p = 20 \times 10^{-6}\text{ Pa} \cdot 10^3$$$$p = 20 \times 10^{-3}\text{ Pa} = 20.0\text{ mPa}\text{ (millipascals)}$$
### 2. Calculate Microphone Output Voltage ($V_{\text{mic}}$)
The microphone sensitivity is $S = 10\text{ mV/Pa}$ ($0.010\text{ V/Pa}$).$$V_{\text{mic}} = p \times S$$$$V_{\text{mic}} = 0.020\text{ Pa} \times 10\text{ mV/Pa} = 0.20\text{ mV}\text{ (or } 0.00020\text{ V)}$$
### 3. Calculate Required Gain in Decibels ($\text{Gain}_{\text{dB}}$)
To boost the mic voltage ($V_{\text{mic}} = 0.20\text{ mV}$) up to line-level ($V_{\text{line}} \approx 1.2\text{ V}$):
$$\text{Gain}_{\text{dB}} = 20 \cdot \log_{10}\left(\frac{V_{\text{line}}}{V_{\text{mic}}}\right)$$$$\text{Gain}_{\text{dB}} = 20 \cdot \log_{10}\left(\frac{1.2\text{ V}}{0.00020\text{ V}}\right)$$$$\text{Gain}_{\text{dB}} = 20 \cdot \log_{10}(6000)$$$$\text{Gain}_{\text{dB}} = 20 \cdot 3.77815 \approx +75.56\text{ dB} \approx \mathbf{+76\text{ dB}}$$


# p13
![[Pasted image 20261103165111.png]]




































































































































