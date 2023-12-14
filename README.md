# Marigold depth estimation in ComfyUI

![image](https://github.com/kijai/ComfyUI-Marigold/assets/40791699/266f6eb4-ec9c-4c25-bdb9-4c1da97bd9be)

This is a wrapper node for Marigold depth estimation:
https://github.com/prs-eth/Marigold

Join us at the [Banodoco Discord](https://discord.gg/xAkA6NTyA3) for discussion on the use and node development:
https://discord.com/channels/1076117621407223829/1184863853096484865

What I know of the parameters so far:

`denoise_steps`: steps per depth map, increase for accuracy in exchange of processing time

`n_repeat`: amount of iterations to be ensembled into single depth map, increase for accuracy in exchange of processing time

`n_repeat_batch_size`: how many of the n_repeats are processed as a batch, if you have the VRAM this can match the n_repeats for faster processing

`invert`: marigold by default produces depth map where black is front, for controlnets etc. we want the opposite

regularizer_strength, reduction_method, max_iter, tol (tolerance) are settings for the ensembling process, don't fully know how to use them yet.

It can pretty memory hungry, and slow, the original local example uses 768p as max resolution (unsure of the hugginface demo).
After some optimizations I've been able to do 2048x2048 without any downscaling with 20GB VRAM.

## Installing:
Recommended way: 

Use the ComfyUI manager (search for "marigold")

Manual install:

Clone this repo to `ComfyUI/custom_nodes`
Install requirements: `pip install -r requirements.txt`

Get the model:

Currently using the same diffusers pipeline as in the original implementation, so in addition to the custom node, you need the model in diffusers format:

https://share.phys.ethz.ch/~pf/bingkedata/marigold/Marigold_v1_merged.tar

Either extract this archive, or do `git clone https://huggingface.co/Bingxin/Marigold/` in either of these folders:

`ComfyUI\custom_nodes\ComfyUI-Marigold\checkpoints`  or `ComfyUI\models\diffusers`
