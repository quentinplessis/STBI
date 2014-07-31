STBI : Read / write images
=====

Read :

``` cpp
string filename = "";
unsigned char* image;
int width, height, n;
int forceChannels = 4;
image = stbi_load(filename.c_str(), &width, &height, &n, forceChannels);
```

Write :

``` cpp
unsigned char* buffer; // data
string filename = "";
int width = 640;
int height = 480;
unsigned char* last_row = buffer + (width * 3 * (height - 1));
if (!stbi_write_png(filename.c_str(), width, height, 3, last_row, -3 * width)) {
  cerr << "ERROR: could not write image to " << filename << endl;
}
```

Write from OpenGL frame buffer :

``` cpp
int width = 640;
int height = 480;
unsigned char* buffer = (unsigned char*) malloc(width * height * 3);
glReadPixels(0, 0, width, height, GL_RGB, GL_UNSIGNED_BYTE, buffer);
// then as above
free(buffer);
```
