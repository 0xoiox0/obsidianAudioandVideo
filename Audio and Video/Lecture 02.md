# p7
![[{7E69856E-C1AC-4A39-A3B7-EE250BDBA5A7}.png]]
==🔵power-of-2 buffer size B:== buffer size必须是2的幂次方


# p13
![[{C67E7180-9D16-43BB-8515-6338239FB294}.png]]
**问题：Step是什么？**
模拟信号是连续的，而数字系统只能用有限的离散数值来表示它。系统会将整个信号的满量程（Full Scale, 简称 FS）纵向切割成若干个等高的“台阶”（即离散电平 Levels）。**每一个台阶的高度，就是量化步长（Step）**。
在图中当前的设置下：
- **位深 $N = 3$**，总共产生 $2^3 = 8$ 个离散电平（Levels）。
- 如果把模拟正弦波的峰峰值全量程（通常归一化为从 $-1$ 到 $+1$，总跨度为 2）平均分给这些台阶：$$\text{Step} = \frac{\text{全量程总跨度}}{\text{级数}} = \frac{2}{8} = 0.250$$
- 因此，图标中显示的 **`0.250`** 意为：**单个台阶的高度占据了整个满量程幅度的 $25\%$（即 $\frac{1}{4}$）**。
如果换到 **16-bit（CD音质）**，在音频和电子工程中，“全量程（Full Scale）”通常指信号从**正峰值到负峰值的整个总跨度**（比如 $-1$ 到 $+1$，总跨度为 **2**）。
- 总跨度 $= 2$
- 级数 $= 2^{16} = 65,536$
- 计算公式：$$\text{Step} = \frac{\text{全量程总跨度 (2)}}{\text{总级数 (65,536)}} = \frac{2}{65,536} \approx 3.05 \times 10^{-5} \approx \mathbf{3.1 \times 10^{-5}}$$

# p14
![[{AE900DC6-4F6F-4918-AFB6-F4B6AA348F31}.png]]
**问题：50 dB, 98 dB, 146 dB是怎么算出来的？**
$$\text{DR} = 6.02 \cdot N + 1.76\text{ dB}$$

**问题：what is rounding noise？**
- **The Rounding Process:** Because a digital system has a limited number of steps (determined by its bit depth), it cannot record the exact, infinite values of an analog wave. Instead, it must "round" each sample to the nearest available digital step.
- **The Resulting Noise:** The tiny difference between the original analog value and the rounded digital value creates an error. When listened to, this error manifests as a subtle hiss or distortion known as rounding/quantization noise.
- **How to Reduce It:** Increasing the bit depth (e.g., moving from 8-bit to 16-bit) increases the number of steps, making the steps much smaller, which pushes the rounding noise down to a much quieter level.

**问题：The rounding noise is at 70 dB SPL什么意思？**
- **What it means:** **"The rounding noise is at 70 dB SPL"** means the absolute loudness of the quantization (rounding) noise has reached 70 decibels of sound pressure level.
- **Why it happens:** Quantization error creates a "noise floor" below the maximum signal. If your maximum playback level is 120 dB SPL and your bit depth provides a limited dynamic range (e.g., 50 dB for 8-bit), the noise floor sits at 120−50=70 dB SPL120 - 50 = 70\text{ dB SPL}120−50=70 dB SPL.
- **Practical impact:** 70 dB SPL is quite loud (comparable to normal conversation or a vacuum cleaner). You would hear a loud, audible hiss even during quiet passages, significantly degrading audio quality.
### 1. 什么是舍入噪声（Rounding Noise）？
在数字音频中，把连续的模拟信号转换成离散的数字信号（量化）时，由于数字位深有限，真实的样点值往往无法被精确记录，必须“四舍五入”到最接近的离散台阶上。这种舍入带来的微小误差，在听感上就表现为量化噪声（Quantization Noise）或舍入噪声。
### 2. 这里的 “70 dB SPL” 是怎么来的？
这是一个绝对响度（Sound Pressure Level）的指标，它取决于两个因素：
- **系统的动态范围（由位深决定）**：比如在较低的位深（如 8-bit，其动态范围约为 $50\text{ dB}$）下。
- **最响播放电平（Loudest Playback Level）**：假设你把系统的最大音量开到了 $120\text{ dB SPL}$。
- **噪声底线的计算**：如果动态范围是 $50\text{ dB}$，意味着最响的声音是 $120\text{ dB}$，那么噪声底线（噪声所在的位置）就会在 $120 - 50 = 70\text{ dB SPL}$。
### 3. 在实际听感中这意味着什么？
- **$70\text{ dB SPL}$ 是一个相当吵闹的响度**：在现实生活中，$70\text{ dB}$ 大约相当于**嘈杂的办公室、正常交谈的说话声、或者开着吸尘器的音量**。
- 如果你的数字音频系统把舍入噪声放大到了 $70\text{ dB SPL}$，这就意味着：**即使在没有音乐信号的静音段，你也能听到非常明显的“嘶嘶”声（量化噪声），甚至会严重干扰甚至淹没音乐中那些极轻柔的细节。**
- （相比之下，在上一张图里介绍的 16-bit CD 音质中，因为动态范围高达 $98\text{ dB}$，如果最大音量设为 $120\text{ dB}$，其舍入噪声底线会被压低到 $120 - 98 = 22\text{ dB SPL}$，远低于安静房间的背景噪声，人耳就听不见了。）


# p16
![[Pasted image 20261107135728.png]]
**问题：mix two identical tracks, what will happen?**
When you combine two **identical** tracks (meaning they are sample-for-sample copies playing at the exact same time and completely in phase), their waveforms undergo perfect **constructive interference**:
1. **Sample-for-Sample Addition:** At any given moment, the digital sample value of Track A is added directly to the identical sample value of Track B ($x + x = 2x$).
2. **Amplitude Doubling:** Because the values double, the physical height of the combined waveform (its peak amplitude) is multiplied by 2.
3. **The +6 dB Result:** As we calculated earlier, applying that $2\times$ amplitude increase to the decibel formula ($20 \log_{10}(2)$) results in a **+6 dB** jump in volume.
_(Note: This only happens with identical, phase-locked copies. If the tracks are different instruments or have independent performances, their phases are uncorrelated, so they sum in power instead of amplitude, resulting in only a **+3 dB** increase per doubling.)_
**Different Tracks:** Different sounds (like guitars and vocals) have uncorrelated phases, so they add up in **power** ($10 \log_{10}(2)$), resulting in an increase of **+3 dB** per doubling instead.

问题：DAW是什么？
**DAW** stands for **Digital Audio Workstation**.
It is an electronic system—typically software running on a computer (like Logic Pro, Pro Tools, Ableton Live, FL Studio, or Reaper)—used for **recording, editing, mixing, and producing audio and music**.

**问题：master fader是什么**
- 它是一个控制**整个混音项目最终输出总音量**的滑块（Fader）。
- 无论是你有 2 条、16 条还是 256 条音轨，它们在经过各自的音量调节、效果处理和分轨混音后，最终都要汇聚（Sum）到总线（Master Bus）上。而 Master Fader 就是控制这条总线最后发往声卡、耳机或导出音频文件的总闸门。
- **控制最终输出电平**：如前文的图表所示，当多条音轨叠加导致内部电平超标（例如浮点数引擎中飙升到 $+30\text{ dBFS}$）时，可以通过向下拉动 Master Fader（例如降低 30 dB），把最终输出音量安全地压制在 $0\text{ dBFS}$ 的红线以内。
- **全局总控**：推动 Master Fader 会等比例放大或缩小所有轨道混合后的整体声音，而不会改变各条轨道之间的相对音量平衡（即不会破坏你辛辛苦苦调好的“混音比例”）。

**问题：lower master by 30 dB 什么意思**
**What it means:** **"Lower master by 30 dB"** means reducing the overall volume level of the Master Fader in your DAW by 30 decibels.



# p17
![[{38C24926-48F1-4460-A275-FDE302E2D930}.png]]
这张图表对比了在数字音频工作站（DAW）中使用浮点数（Float）计算的两个核心优势，分别对应两个常见痛点：
### 1. 问题一：混音内部过载（左侧：The Mix Gets Too Loud Inside）
- **场景**：当你向混音中添加了 8 条音轨（每条峰值为 $-12\text{ dBFS}$）。
- **结果**：由于同相叠加，最坏情况下的峰值达到了 **$+6.1\text{ dBFS}$**，超出了 $0\text{ dBFS}$ 的硬顶。
- **整数（16-bit integer）vs 浮点数（Float）**：
    - **整数**：超出的波形会被直接在中间环节切断（Cut at 0 dBFS），造成**永久性削顶失真（Clipped）**。
    - **浮点数**：完美保存超标数据，只需在最后将主推子调低（`ok, lower the master`），没有任何损失。
- **公式复习**：相同音轨相加遵循压强叠加公式 $20 \cdot \log_{10}(N)\text{ dB}$，而不同音轨增加较少（$10 \cdot \log_{10} N\text{ dB}$）。
### 2. 问题二：录音声音太小后续需大幅放大（右侧：The Recording Was Too Quiet）
- **场景**：录音时忘记开大增益，导致录音电平极低（只有 **$-60\text{ dBFS}$**），事后必须把音量大幅拉高。
- **整数（16-bit integer）vs 浮点数（Float）**：
    - **整数**：因为是固定步长，音量太小时只占用了极少数的量化台阶（此时 16-bit 整数只剩下 33 个可用步骤/级）。放大后声音会变得极其粗糙、充满量化噪声。
    - **浮点数**：由于采用“数值 + 阶码（Scale）”的动态结构（Float32 包含 1 个符号位、8 个指数位、23 个尾数位，共 24 位有效精度），即使信号极小，放大后依然能保持 24 位的细腻细节（`24 bit of detail`）。

# p18
![[{C3AF0330-416D-45DE-A0A5-C684E8C23AA4}.png]]
左右两侧的本质区别：
- **左侧（DAW / float32, $\pm 8$）**：
    - 在 DAW 内部使用 32-bit 浮点数运算时，它的数值范围可以远超 $\pm 1$（即 $\pm 0\text{ dBFS}$ 的红线）。
    - 图中显示，由于音轨增益开到了 **$+21\text{ dB}$**，内部峰值达到了 **$+15.0\text{ dBFS}$**，波形虽然冲破了红线，但 DAW 完美地将其保留了下来（`Float kept the information`）。
- **右侧（Converter / $\pm 1.4$）**：
    - 现实中的声卡/数模转换器（DAC）或最终输出文件（如普通的 16-bit/24-bit 整数音频文件）**没有**浮点数的指数扩展能力，它们的物理极限就是 $\pm 1$（即 $0\text{ dBFS}$ 的硬墙）。
    - 如果直接把 $+15\text{ dBFS}$ 的信号送给声卡，转换器会直接将其削顶（Clip）。
    
解决方案：如何通过转换？
- **勾选框（Pull the master fader down by the same amount）**：
    - 图中勾选了联动选项。当音轨增益提升了 $+21\text{ dB}$（导致内部峰值 $+15\text{ dBFS}$）时，主推子（Master Fader）会自动或手动向下补偿，使得最终送到声卡转换器的峰值被压制在 **$-6.0\text{ dBFS}$**（安全区内）。
- 底部原理解读：
     **"Float32 keeps 24 bit mantissa + 8 bit exponent: values above $\pm 1$ are stored and can be scaled back. The converter has a hard wall at $\pm 1$."** （32位浮点数由 24 位尾数和 8 位指数组成：$\pm 1$ 以上的数值可以被完整存储并随时按比例缩小；但硬件转换器在 $\pm 1$ 处有一堵无法逾越的硬墙。）
**问题：mantissa是什么？**
A floating-point number splits a value into two main components, similar to scientific notation (like $1.23 \times 10^4$):
- **The Mantissa ($1.23$):** Determines the **precision**. It dictates how many fine details and distinct steps you can capture.
- **The Exponent ($10^4$):** Determines the **scale** or **magnitude**. It shifts the decimal point left or right, allowing the number to become massive or microscopic.

# p19
![[{B8C0E7D8-65D9-432A-9650-F77D23922E41}.png]]

The total data rate ($R$) per second is calculated by multiplying three factors:$$\text{Data Rate } (R) = f_s \times N \times C$$
- **$f_s$ (Sampling Rate / samples per second):** How many times per second the analog wave is sampled (e.g., $48,000\text{ Hz}$).
- **$N$ (Bits per Sample):** The bit depth or precision of each sample (e.g., $24\text{ bits}$).
- **$C$ (Channels):** The number of audio channels, where $1 = \text{mono}$ and $2 = \text{stereo}$.

Real-World Hardware Context：
- A standard **USB 2.0** connection has a bandwidth of $480\text{ Mbit/s}$.
- Dividing that by this stream's bit rate shows that USB 2.0 can easily carry **about 125 such stereo audio streams simultaneously** in practice.


# p20

![[{5EF303E5-15EF-4B05-A463-D33F120215B3}.png]]

问题：what is playback?
In the context of digital audio and DAWs, **playback** refers to the process where the computer or audio device reads existing stored audio data (such as prerecorded tracks, instruments, or backing tracks) and converts it back into sound so you can listen to it through your headphones or speakers.

问题：what is backing track?
A **backing track** is a pre-recorded audio accompaniment—such as a rhythm section, instrumental arrangement, or vocal harmony—that plays in the background while a musician or singer performs live over it.
For example, when a vocalist is recording a new part, the backing track provides the instrumental music in their headphones so they can sing in time and in key with the rest of the arrangement.


# p21
![[{2511915A-3D69-40E9-B81E-31A4C8EB8A51}.png]]
**问题：what is callback?**
a **callback** is a function or trigger executed automatically by the audio driver or operating system at regular, strict time intervals to process a new block of audio data.

**问题：what is modulo?**
**Modulo** (often represented by the `%` symbol in programming) is a mathematical operation that finds the **remainder** after dividing one number by another.
Why is it used in Ring Buffers?
As shown in the ring buffer diagram, modulo arithmetic is the secret tool used to make a fixed-size array act like an **endless circle**.
- Imagine your ring buffer has a fixed size of **$L = 16$ slots** (indexed from 0 to 15).
- As the read or write pointer moves forward, the index increases: $14, 15, \dots$
- When the pointer reaches the very end (slot 15) and needs to move forward by one step, the formula uses modulo: `(index + 1) % 16`.
- `(15 + 1) % 16 = 16 % 16 = 0`.
Instead of going out of bounds or crashing the program, the modulo operation automatically wraps the index **seamlessly back to `0`**, allowing the pointer to loop endlessly around the circle.

**问题：what is bucket brigade**
Historically, before modern fire trucks and hoses, a **bucket brigade** was a line of people standing in a row between a water source and a fire.
- Person A scoops water into a bucket and hands it to Person B.
- Person B passes it to Person C, and so on down the line, until the last person dumps it onto the fire.
- Everyone works in synchronized steps, passing discrete units of water from one hand to the next without spilling.

**问题：这里的Delay指的是什么delay？**
In this context, it represents **the time lag between when the computer program writes a block of audio data into the ring buffer and when the hardware DAC actually reads it out** to convert it into physical sound waves.


**解读公式：**$\text{Delay} = \text{fill} \div \text{hardware rate}$
Breaking Down the Components:
- **$\text{fill}$**: The number of audio slots (samples) currently waiting in the ring buffer.
- **$\text{hardware rate}$ (or $\text{clock}$)**: The speed at which the hardware clock consumes those samples, measured in samples per second (Hz)—for example, $48,000\text{ samples/second}$.

Dimensional Analysis (Why the math works):
If you divide the total number of waiting samples by the number of samples processed per second, the "samples" unit cancels out, leaving you with **seconds** (latency/delay):$$\text{Delay} = \frac{\text{samples}}{\left(\frac{\text{samples}}{\text{second}}\right)} = \text{seconds}$$$$callback \ deadline: \ t = \frac{B}{f_s} $$
A Quick Example:
- Suppose your ring buffer currently has a fill level of **$4,800$ samples** waiting.
- Your audio interface is running at a sampling rate of **$48,000\text{ Hz}$** ($48,000$ samples per second).
- $\text{Delay} = \frac{4800}{48000} = \mathbf{0.1\text{ seconds}}$ (or $100\text{ milliseconds}$).


**解读：a bigger fill is safer and later.**
- A **higher fill level** gives the computer more breathing room to process blocks without risking a dropout, but it increases this buffer delay.
- A **lower fill level** reduces the latency (making things more responsive for real-time monitoring), but brings the system dangerously close to an underrun if the computer gets busy.

**问题：what is dropout？**
- If the computer's CPU gets too busy and fails to write the next block of audio data into the ring buffer in time, the buffer empties out.
- Because the hardware clock never waits, it attempts to read from an empty buffer, resulting in missing data and an audible glitch (a dropout).


# p23
![[{C25A68E7-535F-4747-A749-0C9616E333ED}.png]]
问题：what is callback?
- **The Trigger:** Instead of your DAW continuously asking for audio data whenever it wants, the system's audio driver says, _"Time's up! Give me the next block of 4 samples right now."_ and calls your function.
- **Block-Based Processing:** Every time the callback is triggered, your program handles one block of audio data (writing new output or reading input) before going idle until the next timer tick.
- **The Danger of Being Late:** If the computer gets too busy and fails to finish processing the audio within that tiny window, it causes a "late callback," leading directly to a buffer underrun and an audible dropout/glitch.
![[Pasted image 20261107181600.png|192]]
就是这张图片里每次callback，cpu就往buffer里写入（r prog）三个slot

**Callback Deadline ($B / f_s$):** $\frac{256}{48,000\text{ Hz}} = \mathbf{5.33\text{ ms}}$. This means the computer has a strict window of **5.33 milliseconds** to finish processing an entire block of 256 samples before the hardware demands the next one.

**公式：**
$$\text{CPU load} = \frac{\text{overhead per callback}}{\text{buffer time}} + \text{processing share}$$

# p24
![[{0507E271-F3EC-44C3-A2D8-EF9D95678B29}.png]]

### 1. Different Signals (Uncorrelated Power Addition: +3 dB)
- **What it means:** When you add two independent, uncorrelated sound sources (such as two different people talking or two separate background noises), their **acoustic powers add together**.
- **The Math:** Doubling the power means multiplying it by 2. In decibels, power scales by $10 \cdot \log_{10}(2)$, which equals **+3.0 dB**.
- **General Rule for $N$ sources:** The increase is calculated as $10 \cdot \log_{10} N$ (e.g., 4 sources add $+6\text{ dB}$, 16 sources add $+12\text{ dB}$).
### 2. Identical Signals (Coherent Pressure Addition: +6 dB)
- **What it means:** When you combine two **identical** signals that are completely in phase ($\phi = 0^\circ$)—such as duplicating a 440 Hz sine wave track in your DAW—you are adding sound **pressures** rather than just powers.
- **The Math:** Because sound intensity (power) is proportional to the _square_ of sound pressure ($I \propto p^2$), doubling the pressure quadruples the power ($2^2 = 4$). In decibels, pressure scales by $20 \cdot \log_{10}(2)$, which equals **+6.0 dB**.
- **General Rule for $N$ sources:** The increase for identical in-phase sources scales by $20 \cdot \log_{10} N$ (e.g., 4 identical sources add $+12\text{ dB}$).
- **Phase Cancellation:** As noted on the slide, if two identical signals are shifted by **$180^\circ$ out of phase**, their waveforms invert and completely cancel each other out, resulting in total silence.
### 3. The General Combination Formula
#### Formula 1: Uncorrelated Power Addition (Random Phase / Different Signals)
$$L = 10 \cdot \log_{10}\left(10^{L_a / 10} + 10^{L_\beta / 10}\right)$$
- **What it assumes:** The two sound signals are **uncorrelated** (e.g., two different voices, background noises, or unrelated instruments).
- **Why it works:** Because the phase relationship between two independent signals shifts randomly over time, the average interference term $\cos\varphi$ averages out to **zero**.
- **Key Behavior:** Combining two equal independent sources ($L_a = L_\beta = 80\text{ dB}$) results in a **+3 dB** boost ($83\text{ dB}$).
- **Derivation link:** It comes directly from converting each decibel level back to sound intensity/power ($I \propto 10^{L/10}$), adding the powers together ($I_{\text{total}} = I_a + I_\beta$), and converting back to decibels.

#### Formula 2: General Wave Interference (Coherent Signals with Phase $\varphi$)$$L = 10 \cdot \log_{10}\left(p_a^2 + p_\beta^2 + 2 p_a p_\beta \cdot \cos\varphi\right)$$
- **What it assumes:** The sound sources are **coherent** (e.g., identical or phase-locked signals, such as the same sine wave split into two speakers or a single instrument recorded with two microphones).
- **Why it works:** It uses physical sound pressures ($p_a$ and $p_\beta$) and accounts for the **exact phase difference ($\varphi$)** between the arriving sound waves.
- **Key Behavior:**
    - **In Phase ($\varphi = 0^\circ, \cos\varphi = 1$):** Pressures add directly ($p_a + p_\beta$). For two equal sources, this quadruples the power ($2^2 = 4$), giving a **+6 dB** boost.
    - **Out of Phase ($\varphi = 180^\circ, \cos\varphi = -1$):** Pressures subtract ($p_a - p_\beta$). For two equal sources, this yields $0$, causing **complete phase cancellation**.

# p25
![[{6DB96A17-8558-4F56-8D86-6A21EA07992F}.png]]

**问题：what is notch**
Imagine plucking a guitar string or playing a pure tone through two speakers where one speaker is slightly delayed.
1. **At some frequencies**, the delay causes the two sound waves to arrive perfectly matched. They reinforce each other, creating a high point (a **peak**).
2. **At other frequencies**, that exact same time delay causes the two waves to arrive completely out of step (one is pushing up while the other is pulling down). They fight each other and cancel out.
When they cancel out, the volume at that specific frequency plummets straight down toward negative infinity. On the graph, that sudden, sharp drop looks like a V-shaped hole or a "bite" taken out of the line. Audio engineers call that dip a **notch**.





# p26
![[{19AEFDE5-B32C-4A9A-B47C-BCA107AD40EA}.png]]
This slide illustrates the **Distance Law** (commonly known as the inverse-square law for sound), which describes how sound volume drops as you move further away from a sound source in an open, obstacle-free environment (a free field).
### 1. The Core Rule: -6 dB Per Doubling
- Every time you **double the distance** from a point source, the sound pressure level decreases by **6 dB**.
- **Example from the slide:**
    - At a distance of **1 meter**, the sound level is **75 dB SPL**.
    - If you double the distance to **2 meters**, the level drops by 6 dB to **69 dB SPL**.
    - If you double it again to **4 meters**, it drops another 6 dB to **63 dB SPL**, and so on.
### 2. The Ten-Time Rule
- While doubling the distance reduces the volume by **6 dB**, increasing the distance by **ten times** reduces the volume by **20 dB**.
### 3. The Mathematical Formula
The slide presents the formula used to calculate this drop:
$$L(r) = L_1 - 20 \cdot \log_{10}\left(\frac{r}{1\text{ m}}\right)$$
- **$L(r)$**: The sound level at your new distance ($r$).
- **$L_1$**: The reference sound level measured at 1 meter.
- **$r$**: The distance in meters.
Because distance is plotted on a logarithmic scale on the graph, this inverse-square relationship appears as a straight downward-sloping line.

# p27   
![[{559D42F2-47D5-4546-9C72-2C7857E63498}.png]]

$$L_{\text{dBu}} = 20 \cdot \log_{10}\left(\frac{42.4\text{ mV}}{0.775\text{ V}}\right) = 20 \cdot \log_{10}\left(\frac{0.0424}{0.775}\right) \approx \mathbf{-25.2\text{ dBu}}$$
$$20 \cdot \log_{10}\left(\frac{42.4\text{ mV}}{3.37\text{ mV}}\right) = 20 \cdot \log_{10}(12.58) \approx \mathbf{22\text{ dB}}$$
# p29
![[{3A163818-E7BA-4D97-8076-12F595578190}.png]]
- **有效值电压 $U$ (RMS)**： 根据公式 $\text{dBu} = 20 \cdot \log_{10}\left(\frac{U}{0.775\text{ V}}\right)$：$$+4.0 = 20 \cdot \log_{10}\left(\frac{U}{0.775}\right) \implies 0.2 = \log_{10}\left(\frac{U}{0.775}\right)$$$$U = 0.775 \times 10^{0.2} = 0.775 \times 1.5849 \approx \mathbf{1.23\text{ V}}$$
    完美对应图中的 **$1.23\text{ V}$**。
- **峰值电压 $U_{\text{peak}}$ (Sine wave)**： 对于正弦波，峰值等于有效值的 $\sqrt{2}$ 倍（约 $1.414$ 倍）：$$U_{\text{peak}} = 1.228\text{ V} \times \sqrt{2} \approx \mathbf{1.74\text{ V}}$$
    完美对应图中的 **$1.74\text{ V}$**。
- **dBV 电平**： 由于 $0\text{ dBV} = 1\text{ V}$，$\text{dBV}$ 和 $\text{dBu}$ 之间存在固定差值 $\mathbf{2.22\text{ dB}}$（即 $20 \cdot \log_{10}(1 / 0.775)$）：$$\text{dBV} = \text{dBu} - 2.22 = +4.0 - 2.22 = \mathbf{+1.78 \approx +1.8\text{ dBV}}$$
    完美对应图中的 **$+1.8\text{ dBV}$**。
- **数字映射换算（dBu $\rightarrow$ dBFS）**
右侧下拉菜单选择了 **Alignment A = +18 dBu (EBU R68)** 标准，即设置 $A = +18\text{ dBu}$（当模拟输入达到 $+18\text{ dBu}$ 时，数字端刚好达到满量程 $0\text{ dBFS}$）。
根据图中给出的映射公式：$$\text{dBFS} = \text{dBu} - A$$代入当前数据：$$\text{dBFS} = +4.0\text{ dBu} - 18\text{ dB} = \mathbf{-14.0\text{ dBFS}}$$完美对应图中的 **$-14.0\text{ dBFS}$**！

# p30
![[{5155EA78-7D8B-4731-B9F5-CF430108374B}.png]]

### 1. 空气域（Air）：$80\text{ dB SPL} \rightarrow 0.200\text{ Pa}$
- **基准定义**：$94\text{ dB SPL}$ 对应的声压正好是 $1\text{ Pa}$（因为 $20 \cdot \log_{10}(1\text{ Pa} / 20\,\mu\text{Pa}) = 94\text{ dB}$）。
- **计算声压**：$$\text{Level (re } 1\text{ Pa)} = 80\text{ dB SPL} - 94\text{ dB} = \mathbf{-14\text{ dB re } 1\text{ Pa}}$$$$p = 10^{-14 / 20} = 10^{-0.7} \approx \mathbf{0.200\text{ Pa}}$$对应图中的 **$0.200\text{ Pa}$**。
### 2. 话筒域（Microphone）：$0.200\text{ Pa} \rightarrow -54.0\text{ dBV}$
- **麦克风灵敏度**：设置面板为 $10\text{ mV/Pa}$（即每 $1\text{ Pa}$ 声压输出 $10\text{ mV}$ 电压）。
- **计算输出电压**：$$V_{\text{mic}} = 0.200\text{ Pa} \times 10\text{ mV/Pa} = \mathbf{2.00\text{ mV}} = 0.002\text{ V}$$
- **换算为 dBV**（以 $1\text{ V}$ 为基准）：$$\text{dBV} = 20 \cdot \log_{10}\left(\frac{0.002\text{ V}}{1\text{ V}}\right) = 20 \cdot (-2.6989) \approx \mathbf{-54.0\text{ dBV}}$$
- **换算为 dBu**（以 $0.775\text{ V}$ 为基准，固定加 $2.22\text{ dB}$）：$$\text{dBu} = -54.0 + 2.22 = \mathbf{-51.8\text{ dBu}}$$
    完美对应框内的 **$2.00\text{ mV}, -51.8\text{ dBu}$**。
### 3. 话放域（Preamp Output）：$-51.8\text{ dBu} \rightarrow 11.7\text{ dBu}$
- **增益设置**：滑块设定的 Preamp gain 为 **$+63.5\text{ dB}$**。
- **计算放大后的电平**：$$\text{Preamp Out} = \text{Mic Input (dBu)} + \text{Gain} = -51.78\text{ dBu} + 63.5\text{ dB} = \mathbf{11.72 \approx 11.7\text{ dBu}}$$
    完美对应框内的 **$11.7\text{ dBu}$**。
### 4. 转换器域（Converter）：$11.7\text{ dBu} \rightarrow -6.3\text{ dBFS}$
- **对齐标准**：系统采用 EBU R68 标准，即 $0\text{ dBFS} = +18\text{ dBu}$（对齐系数 $A = 18\text{ dB}$）。
- **计算数字电平**：$$\text{dBFS} = \text{Preamp Out (dBu)} - A = 11.72\text{ dBu} - 18\text{ dB} = \mathbf{-6.28 \approx -6.3\text{ dBFS}}$$完美对应框内的 **$-6.3\text{ dBFS}$**。


# p31
![[{1A60EAD2-8FB3-4864-A854-2B10D5DB5A63}.png]]









# p32
![[{3D2A988C-A2D7-439A-AEE1-1456AAFB24F1}.png]]

## **问题：what is snare？**
指的是**军鼓**（或称小军鼓），它是现代架子鼓（Drum kit）中最核心、最具辨识度的打击乐器之一。



# p33
![[{489B71C4-D664-4F43-99E3-E9AFED13455B}.png]]
- [ ] 待做



# Backup
![[{3B0CF6C6-C221-4E69-9F98-E8A534B50D96}.png]]
## **问题：what is plugin chain?**
### 1. 它是如何工作的？（串联信号流）
音频信号在插件链中是**按先后顺序依次流过**的：
- 声音首先进入第一个插件（比如 EQ），被修剪掉不需要的频段。
- 第一个插件处理完后的输出，会直接变成第二个插件（比如压缩机）的输入。
- 这样一环扣一环，直到流出整个插件链。正因如此，插件的**排列顺序**非常重要（例如在压缩前进还是后退加 EQ，声音效果完全不同）。
### 2. 它对 CPU 性能意味着什么？
正如我们刚才在计算 CPU 负载时涉及的例子（“一个插件链在每个回调周期内需要耗时 $0.9\text{ ms}$”），插件链对计算机来说是一个**纯粹的算力负担**：
- 链条里的**每一个插件**都需要运行复杂的数学算法（DSP）来实时处理音频数据。
- 插件越多、或者某个插件的算法越复杂（例如高过采样、高精度母带限幅器），它在每个缓冲区周期内消耗的计算时间（分子）就会越长。
- 如果整个插件链的累积耗时超过了系统的硬性死线（Deadline），就会导致 CPU 负载飙升至 $100\%$ 并产生爆音。
简单来说，插件链就是你给声音施加的一系列“美颜和特效”工序，但工序越多、越复杂，对计算机处理器的实时响应能力要求就越高。

## **问题：what is interleaved stereo**
### 1. Interleaved vs. Non-Interleaved (Split)
- **Interleaved (Stereo):** The samples are written sequentially as a single block of data: `[L1, R1, L2, R2, L3, R3...]`. This is the standard format used by almost all audio files (like WAV, MP3, FLAC) and standard audio hardware buffers because a single pointer can read both channels simultaneously.
    
- **Non-Interleaved / Multi-Mono (Split):** The channels are kept completely separate in memory or storage as two independent blocks: all left channel samples first (`[L1, L2, L3...]`), followed by all right channel samples (`[R1, R2, R3...]`). This is sometimes used internally within certain Digital Audio Workstations (DAWs) or plugin architectures for independent multi-channel routing.
### 2. How it Appears in Buffer Calculations
As we saw in the buffer memory calculation earlier:$$\text{Total Bytes} = B \times \text{Channels} \times \text{Bytes per Sample}$$
Because an interleaved stereo stream packs both channels into the same buffer, you multiply the buffer size ($B$) by **2 channels** to get the total number of samples that need to be processed or transferred at once.
## **问题：why calculate CPU load like this?**
之所以用“实际耗时”去除以“截止时间”（$\frac{0.9\text{ ms}}{1.33\text{ ms}} = 67.5\%$），是因为在实时音频处理中，CPU 的负荷本质上是一个**时间占用比**的问题。
我们可以从以下几个维度来理解这个除法公式的物理意义：
### 1. 周期性的“硬性死线（Deadline）”
- **分母（$1.33\text{ ms}$）代表总时间窗口**：因为缓冲区大小和采样率固定了（如 $B=64$，$48\text{ kHz}$），音频硬件会每隔严格的 $1.33\text{ ms}$ 就催促 CPU 一次（产生一次硬件中断/Callback）。这个 $1.33\text{ ms}$ 就是系统给你的**不可妥协的最后期限**。在这段周期内，时间就这么多，用完了这一帧音频就必须交货。
- **分子（$0.9\text{ ms}$）代表实际干活的时间**：你的插件链（EQ、压缩、混响等）跑完这一帧数据，实际花掉了 $0.9\text{ ms}$ 的 CPU 计算时间。
### 2. 为什么是“实际耗时 ÷ 总时间”？
这和计算日常工作负荷的逻辑完全一样：$$\text{CPU 负荷} = \frac{\text{CPU 实际用于计算音频的时间}}{\text{系统规定的总周期时间}}$$
- 如果你花光了所有的可用时间（$1.33\text{ ms} \div 1.33\text{ ms} = 100\%$），说明 CPU 满载。
- 现在你只花了 $0.9\text{ ms}$，剩下的 $0.43\text{ ms}$ 闲置（用来喘气、处理后台其他软件或系统进程）。
- 把花掉的时间占总时间的比例算出来：$\frac{0.9}{1.33} \approx 67.5\%$，这就是该音频线程在这段周期内的 **CPU 利用率**。




# p37
![[{E2C3745B-A70D-4EA1-A9FB-3ADAA615E1AA}.png]]

## **问题：what is xrun？**
An **xrun** (short for **overrun** or **underrun**) is a critical error in real-time digital audio processing that occurs when the computer's CPU fails to process and deliver audio data within the strict hardware buffer deadline.
The term is a portmanteau combining **"over"** and **"under"** with **"run"**, and it breaks down into two specific scenarios:
### 1. Buffer Underrun (Most Common)
- **What happens**: The audio interface's hardware clock demands the next block of audio samples right on schedule (governed by the callback deadline formula $t = B / f_s$). However, your CPU and plugin chain are still crunching numbers and haven't finished calculating the audio in time.
- **The result**: The output buffer runs dry, resulting in an audible **click, pop, or severe audio dropout**.
### 2. Buffer Overrun
- **What happens**: Incoming audio data (from a recording input) arrives faster than the system can read and process it.
- **The result**: The input buffer fills to capacity and overflows, causing incoming audio samples to be lost or corrupted.

## **红字想表达的信息**
### 1. Level: +3 dB, not twice as loud
- **字面意思**：电平增加 $+3\text{ dB}$，并不等于声音听起来“大了一倍”。
- **核心表达**：
    - **物理层面的翻倍**：在声学和电路中，$+3\text{ dB}$（对应功率或能量翻倍）确实代表物理能量加倍了。
    - **心理声学层面的主观感知**：人耳对声音响度的感知是**对数非线性**的（符合韦伯-费希纳定律）。要把主观听觉上的响度觉得“大了一倍”，物理电平通常需要提升约 **$+10\text{ dB}$**。因此，千万不要把物理能量的翻倍（$+3\text{ dB}$）和人耳听觉的响度混为一谈。
### 2. Bits: float ≠ converter
- **字面意思**：数字音频工作站（DAW）内部的浮点数运算，不等于物理硬件转换器（ADC/DAC）的实际精度。
- **核心表达**：
    - **DAW 内部（32-bit float）**：拥有极其庞大的内部动态余量（Headroom），内部信号哪怕超过 $0\text{ dBFS}$（例如加到 $+20\text{ dBFS}$）也不会立刻发生硬削顶（Clipping），因为浮点数可以容纳极大的数值范围。
    - **物理硬件端（Converter）**：现实中的模数/数模转换器（ADC/DAC）是由物理电路构成的，有绝对的**硬顶峰（Hard Wall at $\pm1$）**。一旦物理输入或输出超出硬件极限，就会产生不可逆的数字削顶破音。
    - **启示**：不能因为 DAW 内部用浮点数运算很安全，就忽视前端硬件增益级（Gain Staging）的控制。
### 3. Time: t = B / fs
- **字面意思**：单次回调处理的时间窗口，等于缓冲区大小除以采样率。
- **核心表达**：这是实时音频处理的**生命线公式**。
    - $B$（Buffer size，如 64、256 采样点）和 $f_s$（Sample rate，如 48,000 Hz）共同决定了 CPU 必须在多短的时间内（比如 $1.33\text{ ms}$）把一帧音频算完。
    - 它是连接**硬件配置**与**软件计算性能**的唯一桥梁：缓冲区设得越小、延迟越低，CPU 的死线就越苛刻，稍有不慎就会引发 xrun（爆音卡顿）。








































