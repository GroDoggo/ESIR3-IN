Moshen Abdoli, Xiamoï Technology
## Standardization
### Terms
Format = norm = codec = standard (ISO)
H261 - 266 -> MPEG format/standards/norms/codecs
VP8, VP9, AV1 -> non MPEG - AOM (non-standard)
MP4, MKV -> Containers (video + audio + metadata)
### What is it?
The specification
Define a huge set of rules
How the bitstream must be formatted
### Why
We want to be sure that the receiver can always playback the compressed video
Standard define theses rules
-> we call this Inter-operability
We use new standard because we find new techniques to gain more compression
-> 50% gain over 10 years
![[Pasted image 20231212082240.png]]
new format (4k, 8k , 360, ...) can't be formatted (not designed for) with old codec
-> adapt with new formats
### How
MPEG meetings every 3 mouths
Thousands of contributors/contributions
Interest for royalties for company
## High-Level look into video codecs
### Diagram
Input -> Sequence of frames
Process 
-> Decorrelate as much redundancies os possible
-> Represent raw signal in standard
Output -> Bitstream
![[Pasted image 20231212084341.png]]
Intra-frame and inter-frame predictions
Transform and quantization
Loop filter
Entropy coding
### HL view
Basic sources of redundancies
- Spatial : texture
- Temporal : motion
Main steps :
1. Identify redundancies
2. Break signal into correlated parts (divide)
3. Represent each part with decorrelated model (conquer)
### Models
A syntax to represent form of redundancy
Goal -> Decorrelate and represent signal with less bits
![[Pasted image 20231212084938.png]]
**warning** -> bad model can exist (represent with more bits than before)
In codec , we use combination of models to achieve best performances
![[Pasted image 20231212085115.png]]
### Building blocks
Inside a video codec -> hybrid block-based coding sheme
A lot of models :
 - Picture partitioning
 - Pixel prediction (Intra Inter)
 - Residual (Transform/quantization)
 - Quality enhancement filter
#### Partitioning
Each image is split into rectangular blocks (partition map into bitstream)
Order is predefined
![[Pasted image 20231212090317.png]]
http://parabolaresearch.com/blog/2013-12-01-hevc-wavefront-animation.html
More correlation -> pixels within blocks
Less correlation -> pixels between blocks
**Good partitioning lead to good prediction**
#### Prediction
**Spatial** prediction and **temporal** prediction
![[Pasted image 20231212091008.png]]
#### Residual
Improve the prediction
![[Pasted image 20231212091038.png]]
#### Hybrid block-based scheme
Partitioning + Prediction + Residual
### Group of pictures (GoP)
Break video into group of pictures (GoP)
Indépendant picture (the first) -> **Intra-frame** or Q-frame
Dépendant picture (the rest) -> **Inter-frame**
![[Pasted image 20231213130832.png]]
**Warning** Not same order Encode/display
(E, D) -> (Encode order, Display order)
![[Pasted image 20231213131251.png]]
De cette façon, des frames peuvent prédire en utilisant la frame d'avant et après
Can't do with only one intra frame
- Scene change (all content change, nothing we can predict)
- Seek option (if the user change timestamp, we need to go to the nearly Q-frame)
### Intra-frame (Q-frame) prediction
We can only use spatial prediction
IPM set
We need pixels around block (top and left)
![[Pasted image 20231213132550.png]]
Model parameters -> model index (for VVC between 0 and 66)
In more rectangular shape, the angle varies
We choose one angle/IPM per blocks (ALL PIXELS HAVE THE SAME ANGLE)
### Inter-frame prediction
We use temporal prediction
We compute motion of the blocks into motion vector (MV)
![[Pasted image 20231213134026.png]]
### Summary
![[Pasted image 20231213134109.png]]
### Prediction residual
Prediction alone is not enough
We need to send additional signal with same size to correct the signal -> **Residual**
Low entropy
**Example** -> Transformation in another domain
DCT -> any 2D signal w 64 coefficients
Human Visual System (HVS) is less sensitive in High frequencies -> to low frequency is more important
### Lossy compression
![[Pasted image 20231213140638.png]]
Transformation alone is not enough
Bad prediction limits the capacity of transformation
### Filters
Discontinuity between block can be visible (blockiness)
We use deblocking filter
## Decision
Only encoder side
### What is a decision
Informing the receiver about how interpret the bitstream
Represent the smallest number of bits
### Make
*example : we have M models $m_i$*
Each model have $N_i$ parameters:
- IMP is index
- Motion is MV
- Partioning is block width, height
- Residual is Coeff

Decision -> choose optimized parameters
How? Try them all and test (Rate, Distortion) (minimize both)
Generaly in constrast
- High quality -> High bitrate
- Low bandwidth -> Low quality

Cost -> $J_s = D_s + \lambda * R_s$
$\lambda$ decided by user
QP -> Quantization parameters
Large QP -> high distortion during quantification and **lambda diminue**
### Predict
Decisions can be redundant (same decision on part of images)
#### IPM
Most popular index (0, 1, vertical, horizontal)
![[Pasted image 20231214152937.png]]
We can predict index
Create a list of Most Probable Modes (MPM)
if modes in MPM -> signal mode index in MPM
else -> signal index in all IMPs
#### Motion vector MV
MV = <0,0> for most parts (background)
OR MV = <x, y> when camera move (background movement same everywhere)
![[Pasted image 20231214153729.png]]
### Write a decision
Huffman coding with dynamics probabilities
Context-adaptive entropy coding
