Paper: [Learning to Rank Question-Answer Pairs using Hierarchical Recurrent Encoder
with Latent Topic Clustering](https://arxiv.org/pdf/1710.03430.pdf)

Summary: 
- Uses HRED encoder for Context
- Uses RNN encoder for response
- Connects them in Recurrent Dual encoder fashion.
- Novelty: Adds a latent topic clustering module (LTC).
  - Nothing but Attention where input states are now learnable parameters.
  - Idea is that then learned states will represent the latent topics in the dataset.
