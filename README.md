# ecb-penguin
[How AES diffusion (permutation) does not impact ECB penguin pattern with in each block?](https://crypto.stackexchange.com/questions/102107/how-aes-diffusion-permutation-does-not-impact-ecb-penguin-pattern-with-in-each)

##### Answer
If it's a 24-bit image (I'd guess that's the case for the original), a block is a horizontal line of 5.33 pixels. In grayscale areas this equals the effective block size, in colored areas the effective block size will be a horizontal line of 16 pixels.Since the original image is low resolution, large shapes like the penguin itself are preserved, while fine details like the eyes turn to noise. Fillippo's new images are very high resolution, so the 15 pixel wide randomization only covers a very small area, which enables them to preserve even those fine details,


### First convert the Tux to PPM with Gimp
Install [Gimp](https://www.gimp.org/downloads/) > Open `Tux-original.png` image and export as `ppm` in raw format.

### Take header apart
`head -n 4 Tux-raw.ppm > header-raw.txt`

### Take body apart
`tail -n +5 Tux-raw.ppm > body-raw.bin`

### Then encrypt with ECB (experiment with some different keys)
`openssl enc -aes-128-ecb -nosalt -pass pass:"ANNA" -in body-raw.bin -out body-raw-128.ecb.bin`

`openssl enc -aes-192-ecb -nosalt -pass pass:"ANNA" -in body-raw.bin -out body-raw-192.ecb.bin`

`openssl enc -aes-256-ecb -nosalt -pass pass:"ANNA" -in body-raw.bin -out body-raw-256.ecb.bin`

### And finally put the result together and convert to some better format with Gimp

`cat header-raw.txt body-raw-128.ecb.bin > Tux-raw-128.ecb.ppm`

`cat header-raw.txt body-raw-192.ecb.bin > Tux-raw-192.ecb.ppm`

`cat header-raw.txt body-raw-256.ecb.bin > Tux-raw-256.ecb.ppm`

The below images are created with low resolution image and eyes, and other parts of body gets converted into noise. I did not find a very high quality Tux image to test retention of all details but I assume Filippo used a very high resolution image.

### Tux-raw-128.ecb.png
![Tux-raw-128.ecb.png](./Tux-raw-128.ecb.png)

### Tux-raw-192.ecb.png
![Tux-raw-192.ecb.png](./Tux-raw-192.ecb.png)

### Tux-raw-256.ecb.png
![Tux-raw-256.ecb.png](./Tux-raw-256.ecb.png)

### References
The steps to create a ecb penguin is available https://words.filippo.io/the-ecb-penguin/

https://crypto.stackexchange.com/questions/102107/how-aes-diffusion-permutation-does-not-impact-ecb-penguin-pattern-with-in-each

