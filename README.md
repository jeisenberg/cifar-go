# Cifar utility library

### How it works

This is a simple utility library for reading, writing, and encoding images in the [http://www.cs.toronto.edu/~kriz/cifar.html](CIFAR) file format. The files have two components, one byte length of metadata, or 'label', and the rest of the file the bytes of the image.

The simplest way to write an image in this format is to call the function:

```go
/// open an image file
reader, err := os.Open(tmpFile.Name())
if err != nil {
  panic(err)
}
defer reader.Close()
/// get the image.Image
m, _, err := image.Decode(reader)
/// convert your label to a uint8
labelAsUint8 := uint8(1)

// set your filepath
cifarPath := "tmp-cifar/img.bin"
err = cifar.WriteImageAsCifar(m, cifarPath, labelAsUint8)
if err != nil {
  panic(err)
}
```

And that should write a cifar image to the filepath passed in. It's that simple.
