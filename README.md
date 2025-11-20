# mldm_exam_project
Ostudina Kseniia MLDM final project

Model's architecture is absolutly the same as in the article https://arxiv.org/abs/1606.03657 

- z ~ N(0,1), size 62
- c_cat — 10 categories
- c_cont — 2 continuous latent variables
- Full vector: 74
- Generator and discriminator as DCGAN
- The Q-network is built on top of the discriminator, as in the article
- β1 = 0.5, lr = 2e−4 — as in DCGAN/InfoGAN
- λ_MI = 1.0 — as in the appendix to the article
