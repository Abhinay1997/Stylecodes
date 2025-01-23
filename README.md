# Stylecodes
Attempt at recreating CiaraRowles StyleCodes a.k.a opensource midjourney srefs

## Idea

`Encoder -> Stylecode -> Decoder -> Pretrained Diffusion Model -> Image`

* Encoder:
   * Use a strong style prior like CSD or InstantStyle-like SigLIP processed vector.
   * Embeddings from the prior are passed to a MLP to encode to a low-dimensional latent space aka 20 character b64 string.

* Decoder:
   * StyleCodes uses a ControlNet like network which is expensive to train. OminiControl and Flux redux adpater both show how the DiT context space is good for training.
   * Use redux adapter to process the tokens from the style decoder
 
* Pretrained Models:
   * Try Fkux-1 schnell, Sana or Flex-1 Alpha. Faster to iterate over than Flux.
 
## Training   

* Joint Training vs Seperate encoder/decoder training:
  * Joint training helps in better and faster learning but stylecodes and models are tightly coupled.
  * Seperate encoder and decoder training decouples the stylecode from the diffusion model.
 
* Loss:
  * Flow matching loss + cycle consistency loss a.k.a use the same style prior to make sure the style consistency exists.
  * Might need a timestep threshold though.
