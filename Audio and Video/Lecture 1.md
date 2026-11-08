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

# p8
![[{BF7D4EA0-1BB4-4D3D-A25C-E1FC6C8A0493}.png]]
## 功率的分贝公式为 $\Delta L = 10 \cdot \log_{10}\left(\frac{P_2}{P_1}\right)$。
当功率变为 2 倍，即 $\frac{P_2}{P_1} = 2$ 时：
$$\Delta L = 10 \cdot \log_{10}(2)$$
利用常用对数近似值 $\log_{10}(2) \approx 0.3010$：
$$\Delta L = 10 \cdot 0.3010 = \mathbf{+3.01\text{ dB}} \approx \mathbf{+3\text{ dB}}$$
**反向推导**：如果已知增益是 $+3\text{ dB}$，求功率倍数 $\frac{P_2}{P_1}$：
$$3 = 10 \cdot \log_{10}\left(\frac{P_2}{P_1}\right) \implies 0.3 = \log_{10}\left(\frac{P_2}{P_1}\right)$$$$\frac{P_2}{P_1} = 10^{0.3} \approx 1.995 \approx \mathbf{2}$$
## 电压/声压的分贝公式为 $\Delta L = 20 \cdot \log_{10}\left(\frac{U_2}{U_1}\right)$。
当电压变为 2 倍，即 $\frac{U_2}{U_1} = 2$ 时：$$\Delta L = 20 \cdot \log_{10}(2)$$
代入 $\log_{10}(2) \approx 0.3010$：
$$\Delta L = 20 \cdot 0.3010 = \mathbf{+6.02\text{ dB}} \approx \mathbf{+6\text{ dB}}$$
- **反向推导**：如果已知增益是 $+6\text{ dB}$，求电压倍数 $\frac{U_2}{U_1}$：$$6 = 20 \cdot \log_{10}\left(\frac{U_2}{U_1}\right) \implies 0.3 = \log_{10}\left(\frac{U_2}{U_1}\right)$$$$\frac{U_2}{U_1} = 10^{0.3} \approx 1.995 \approx \mathbf{2}$$
1. $\text{dB SPL}$
$$p = 20\ \mu\text{Pa} \cdot 10^{(L/20)}$$
$$L = 20 \cdot \log_{10}\left(\frac{p}{20\ \mu\text{Pa}}\right)$$
**$20\ \mu\text{Pa}$**：参考基准，即人耳能听到的最安静声音（$1\text{ kHz}$ 时的听觉阈值）。

2. $\text{dBu}$
$$\text{dBu} = 20 \cdot \log_{10}\left(\frac{V}{0.775\text{ V}}\right)$$
**$0.775\text{ V}$**：标准参考电压（源于在 $600\ \Omega$ 阻抗电路中产生 $1\text{ mW}$ 功率所需的电压）。

3. $\text{dBFS}$
$$\text{dBFS} = 20 \cdot \log_{10}\left(\frac{A}{A_{\max}}\right)$$
- **$A$**：当前数字信号的实际振幅或样点数值。
- **$A_{\max}$**：数字音频系统能够表示的**最大绝对振幅**（即数字上限/满度值，对应 $0\text{ dBFS}$）。
- **0 dBFS** (Decibels Full Scale) is the absolute maximum limit of a digital audio system. Because digital audio is stored using a fixed number of bits (like 16-bit or 24-bit integers), the system can only represent numbers up to a specific maximum value. When a signal hits this ceiling ($0\text{ dBFS}$), it cannot go any higher. If it tries, the digital system lops off the peaks, causing harsh, distorted digital clipping.

**Example to explain 0 dBFS**
**Setup**: In a 16-bit audio system, the maximum integer value is $A_{\max} = 32,767$, which equals **$0\text{ dBFS}$**.
- **Scenario 1 (Normal Signal)**: If a sample's amplitude is $A = 16,384$ (about half of maximum):$$\text{dBFS} = 20 \cdot \log_{10}\left(\frac{16,384}{32,767}\right) \approx 20 \cdot \log_{10}(0.5) \approx \mathbf{-6.02\text{ dBFS}}$$_Result_: The signal is clean, leaving $6\text{ dB}$ of headroom.
- **Scenario 2 (Clipping)**: If a loud sound tries to reach $A = 40,000$:
    - The 16-bit system cannot store numbers above $32,767$.
    - It forcibly cuts (clips) the value down to $32,767$, outputting **$0\text{ dBFS}$** instead of the intended $+1.73\text{ dBFS}$._Result_: The peak is flattened, causing harsh digital distortion.
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






# p14
![[{A9978B6D-CD72-4E47-8D90-59FDAEFF84B4}.png]]
==🔵Teal==：蓝绿色，青色
==🔵Amber==：琥珀色/橙色

**Nyquist Limit (Highest Safe Tone):** Equal to half of the sampling rate $$f_s / 2$$To accurately capture a signal without distortion, the sampling rate must be strictly greater than twice the highest audio frequency.


Calculate the folded, incorrect frequency that ends up being stored in the digital system:$$f_{\text{stored}} = \vert{}f - k \cdot f_s\vert{}$$$k$ is whole number
- **Explanation**: To find $k$ in the aliasing formula ($f_{\text{stored}} = \vert{}f - k \cdot f_s\vert{}$), you don't need to guess. $k$ represents the multiple of the sampling rate ($f_s$) that the input frequency ($f$) is closest to. You can easily find it by dividing the input frequency by the sampling rate and rounding to the nearest whole number: $k = \text{round}\left(\frac{f}{f_s}\right)$.
- **Example 1**:
    - Given a sampling rate $f_s = 8\text{ kHz}$ and an input tone $f = 4.4\text{ kHz}$:
    - Calculate the ratio: $\frac{4.4}{8} = 0.55$.
    - Round $0.55$ to the nearest whole number, which gives **$k = 1$**.
    - Plug it into the formula: $f_{\text{stored}} = \vert{}4.4 - 1 \cdot 8\vert{} = \vert{}-3.6\vert{} = \mathbf{3.6\text{ kHz}}$.
- **Example 2**:
    - Given a sampling rate $f_s = 8\text{ kHz}$ and an input tone $f = 30\text{ kHz}$:
    - Calculate the ratio: $\frac{30}{8} = 3.75$.
    - Round $3.75$ to the nearest whole number, which gives **$k = 4$**.
    - Plug it into the formula: $f_{\text{stored}} = \vert{}30 - 4 \cdot 8\vert{} = \vert{}-2\vert{} = \mathbf{2\text{ kHz}}$.



# p15
![[{A5469506-599F-4D68-9C6A-3492AD996CB0}.png]]

这个公式的推导可以了解，但是目前认为不必要，直接记公式就行：
$$\text{DR} \approx 6.02 \cdot N + 1.76\text{ dB}$$
**Noise：**
### 1. 尺子刻度的类比
- 想象你在用一把**只有整数厘米刻度**（1cm, 2cm, 3cm...）的尺子去测量一个物体的长度。
- 如果物体的真实长度是 **$2.37\text{ cm}$**：
    - 尺子没有 $0.01\text{ cm}$ 的精细刻度。
    - 你被迫把它“四舍五入”记录为 **$2\text{ cm}$**（或者 $2.4\text{ cm}$）。
- 真实值 ($2.37$) 和你记录的值 ($2.4$) 之间凭空差了 **$0.03\text{ cm}$**。这个由于刻度有限而产生的“对不齐”的差值，就是**量化误差**。
### 2. 为什么它会变成“噪声”（Quantization Noise）？
- 在数字音频中，每秒钟要进行几万次这样的采样。
- 每一个采样点在落到最近的数字“台阶”时，都会产生大大小小、随机波动的偏差（就像前面那张图的下方红线所示）。
- 当你把这些连续的微小误差还原成声音播放出来时，它们听起来并不像规律的音乐，而是一种持续的、像收音机信号不好时的“沙沙”声（底噪/Hiss）**。这就是**量化噪声。

In audio engineering and signal processing, **Dynamic Range** is the decibel difference between the maximum undistorted signal and the minimum discernible signal (background noise floor) that a system can cleanly record, process, or reproduce.
Simply put, it is the span between the "loudest sound" and the "quietest noise floor" that the system can accommodate.
### 1. The Two Boundaries of Dynamic Range
- **Upper Limit (Ceiling / Maximum Signal):**
    - This is the absolute limit the system can withstand. In digital audio, this ceiling is **$0\text{ dBFS}$**. If a sound exceeds this upper limit, the hardware or software cannot contain it, resulting in severe **clipping distortion**.
- **Lower Limit (Floor / Minimum Signal):**
    - This is the system's **Noise Floor**. In digital systems, it consists of quantization noise determined by the **bit depth**; in analog systems, it is caused by circuit thermal noise. If an input sound is too quiet and its amplitude falls below or is submerged in this noise floor, it cannot be clearly distinguished.
### 2. Why Is It Important?
- **Musical Nuance and Depth:** Real-world sounds have an immense dynamic range—ranging from the softest whisper of strings in a symphony (only a few decibels) to the roaring thunder of timpani or brass instruments (exceeding $100\text{ dB}$).
- **The Role of Bit Depth:** As defined by the formula:$$\text{DR} \approx 6.02 \cdot N + 1.76\text{ dB}$$
    The number of bits ($N$) directly dictates the size of the dynamic range:
    - A **16-bit** system provides a dynamic range of approximately **$96\text{ dB}$**.
    - A **24-bit** system can reach up to **$144\text{ dB}$**, allowing it to capture everything from the faintest breath to thunderous instrumental peaks with pristine clarity.

# p16
![[{33C8BABB-1719-4CC3-93B2-CD1B33918650}.png]]

**双向往返延迟（Round trip）**：
- 声音从输入到计算机处理再到输出，通常需要经过输入缓冲区和输出缓冲区，再加上转换器的延迟（约 $3\text{ ms}$）。
- 往返总延迟计算公式：$$\text{Round trip} \approx \frac{2 \cdot B}{f_s} + 3\text{ ms} $$
### 1. 什么是缓冲区（Buffer）？
在数字音频系统中，计算机无法做到“随来随处理”每一个极微小的声音样本，那样会极其频繁地打断 CPU，导致系统不堪重负而产生爆音或卡顿。
- **音频的“临时集装箱”**：缓冲区就像是一个个装货的箱子。声卡将连续不断的音频样本一小批一小批地收集到这个箱子里。等箱子**装满**之后，再统一打包交给电脑 CPU 去处理（比如添加混响、均衡器等效果），处理完后再输出播放。
### 2. 2048 个采样点（Samples）是什么？
- **箱子的容量**：这里的 **2048** 指的是缓冲区的大小（Buffer Size），即这个临时集装箱一次性能容纳 **2048 个音频采样点**。
- **它代表多长时间？**：这取决于当前的**采样率（$f_s$）**。
    - 如果采样率设置为 $48\text{ kHz}$（即每秒钟采集 $48,000$ 个点），那么装满这 2048 个点需要的时间计算如下：$$t = \frac{B}{f_s} = \frac{2048}{48,000\text{ Hz}} \approx 42.7\text{ ms}$$
    - 这意味着单向的缓冲区就会产生约 **$42.7\text{ 毫秒}$** 的滞后。如果算上声音输入、输出以及数模转换的固定延迟，总往返延迟（Round trip）会高达 **$88.3\text{ 毫秒}$**。
### 3. 缓冲区大小如何影响实际工作？
- **大缓冲区（如 2048 采样点）**：
    - **特点**：给计算机 CPU 留出了充裕的处理时间，系统非常稳定安全。
    - **缺点**：延迟太高（接近 $90\text{ ms}$）。如果此时对着麦克风说话或弹吉他，耳机里听到的声音会明显慢半拍，**不适合实时监听（Live monitoring）**。
    - **适用场景**：音乐制作后期的**混音和母带处理**，此时电脑需要加载大量复杂的插件，高延迟完全可以接受。
- **小缓冲区（如 64 或 128 采样点）**：
    - **特点**：延迟极低（几毫秒内），人耳察觉不到滞后，适合歌手录音或乐器演奏时的**实时监听**。
    - **缺点**：CPU 处理压力剧增，如果电脑性能不够，极易导致声音断续或爆音。

# p17
![[Pasted image 20261106233109.png]]













































































































































