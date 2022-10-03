# ecb-penguin

The steps to create a ecb penguin is available https://words.filippo.io/the-ecb-penguin/

### First convert the Tux to PPM with Gimp

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
