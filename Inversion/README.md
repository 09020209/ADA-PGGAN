The pre-trained generator is saved as network-snapshot-000600.pkl
The pre-trained Resnet50 model is saved as image_to_latent_ada.pt
Then find the latents for the real digital rock by using the encode_image.py script.
```bash
python encode_image.py
  aligned_image.jpg
  dlatents.npy # The filepath to save the latents at.
  --save_optimized_image true
```















