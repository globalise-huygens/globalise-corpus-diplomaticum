# Corpus diplomaticum

## Download pdf files
<https://www.cortsfoundation.org/digitheek-en#CD>

## Extract ppm images from pdf files

```bash
mkdir ppm

for file in /path/to/folder/*.pdf; do
  prefix=$(basename "$file" .pdf)
  pdftoppm -r 300 "$file" /path/to/folder/ppm/"$prefix"
done
```

## OCR

Using [Tesseract](https://tesseract-ocr.github.io/) version 5.3.1

```bash
$ tesseract --version
tesseract 5.3.1
 leptonica-1.82.0
  libgif 5.2.1 : libjpeg 8d (libjpeg-turbo 2.1.5.1) : libpng 1.6.39 : libtiff 4.5.0 : zlib 1.2.11 : libwebp 1.3.0 : libopenjp2 2.5.0
 Found SSE4.1
 Found libarchive 3.6.2 zlib/1.2.11 liblzma/5.4.1 bz2lib/1.0.8 liblz4/1.9.4 libzstd/1.5.4
 Found libcurl/7.87.0 SecureTransport (LibreSSL/3.3.6) zlib/1.2.11 nghttp2/1.51.0
```

### TXT

```bash
mkdir txt

for f in images/*.ppm; do
  output_file="txt/$(basename "${f%.ppm}")"
  tesseract "$f" "$output_file" \
  -l nld \
  -c tessedit_char_whitelist="\"-()'’.,1234567890ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz ;:" \
  -c preserve_interword_spaces=1;
done
```


 
