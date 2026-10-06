# Research on Scene 3D Reconstruction ■ 291

11.3.1.2 OutputFormat Similar to InputFormat, the user must implement the OutputFormat and RecordWriter interfaces to determine the user-defined output format. In this system, we use two kinds of OutputFormat, which are included in the Hadoop output library: (1) FileFileOutput writes all the key-value pairs into a single file and (2) MultiOutputFormat writes all the values that have the same key into a file named according to the key.

11.3.2 Scene Reconstruction Pipeline
This section discusses our system, including four MapReduce modules and the input data/output result of each module. In Figure 11.13, we can see the whole reconstruction pipeline.

11.3.3.3 Extract Focal Length
This is the first MapReduce module invoked in our pipeline, and here we assume that all the input images have been uploaded to the HDFS. This step is simple: The image is split into N splits, possibly twice than the map workers. The RecordReader reads the file and the Exif value of each image and then passes to the mapper. In Map function, the system reads the Exif and extracts the focal length of each image exists. Then FileFileOutput collects the name and focal length of each file and invokes RecordWriter to write into a single file for future use.

11.3.3.4 SIFT Detector
Since no source code is provided from SIFT, the only way to apply SIFT on Hadoop is to invoke external file with the appropriate parameters. The command line format probably looks like:

```
$ < $IMAGE_DIR/$PGM_FILE > $KEY_DIR/$KEY_FILE
```

Here, sift is the executable file of SIFT and the $IMAGE_DIR/$PGM_FILE indicates the position of the input pgm file in the file system and the $KEY_DIR/$KEY_FILE defines the position of the output key. If the parameter of ">KEY_DIR/$KEY_FILE" is not existent, sift will output the key to the standard output.

Because our images are mostly jpg images, we must transfer jpg images into pgm images. In our implementation, each input jpg file is treated as a split, and RecordReader will read the whole content of jpg file as value and pass to the mapper. Then two external files are invoked in Map function. First, we throw the content of jpg image into an image transform program and then it will generate a pgm format image. Second, we redirect