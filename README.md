# LZ4 Java

LZ4 compression for Java, based on Yann Collet's work available at
http://code.google.com/p/lz4/.

This library provides access to two compression methods that both generate a
valid LZ4 stream:
 - fast scan (LZ4):
   - low memory footprint (~ 16 KB),
   - very fast (fast scan with skipping heuristics in case the input looks
     incompressible),
   - reasonable compression ratio (depending on the redundancy of the input).
 - high compression (LZ4 HC):
   - medium memory footprint (~ 256 KB),
   - rather slow (~ 10 times slower than LZ4),
   - good compression ratio (depending on the size and the redundancy of the
     input).

The streams produced by those 2 compression algorithms use the same compression
format, are very fast to decompress and can be decompressed by the same
decompressor instance.

## Implementations

For LZ4 compressors, LZ4 HC compressors and decompressors, 3 implementations are
available:
 - JNI bindings to the original C implementation by Yann Collet,
 - a pure Java port of the compression and decompression algorithms,
 - a Java port that uses the sun.misc.Unsafe API in order to achieve compression
   and decompression speeds close to the C implementation.

Have a look at LZ4Factory for more information.

## Compatibility notes

 - Compressors and decompressors are interchangeable: it is perfectly correct
   to compress with the JNI bindings and to decompress with a Java port, or the
   other way around.

 - Compressors might not generate the same compressed streams on all platforms,
   especially if CPU endianness differs, but the compressed streams can be
   safely decompressed by any decompressor implementation on any platform.

# net.jpountz.xxhash Java

net.jpountz.xxhash hashing for Java, based on Yann Collet's work available at
http://code.google.com/p/net.jpountz.xxhash/. net.jpountz.xxhash is a non-cryptographic, extremly fast
and high-quality ([SMHasher](http://code.google.com/p/smhasher/wiki/SMHasher)
score of 10) hash function.

## Implementations

Similarly to LZ4, 3 implementations are available: JNI bindings, pure Java port
and pure Java port that uses sun.misc.Unsafe.

Have a look at XXHashFactory for more information.

## Compatibility notes

 - All implementation return the same hash for the same input bytes:
   - on any JVM,
   - on any platform (even if the endianness or integer size differs).

# Download

You can download released artifacts from [Maven Central](http://repo1.maven.org/maven2/net/jpountz/lz4/lz4/).

# Documentation

 - [lz4](http://jpountz.github.com/lz4-java/1.1.0/docs/net/jpountz/lz4/package-summary.html)
 - [net.jpountz.xxhash](http://jpountz.github.com/lz4-java/1.1.0/docs/net/jpountz/net.jpountz.xxhash/package-summary.html)
 - [changelog](http://github.com/jpountz/lz4-java/blob/master/CHANGES.md)

# Performance

Both lz4 and net.jpountz.xxhash focus on speed. Although compression, decompression and
hashing performance can depend a lot on the input (there are lies, damn lies
and benchmarks), here are some benchmarks that try to give a sense of the
speed at which they compress/decompress/hash bytes.

 - [lz4 compression](http://jpountz.github.com/lz4-java/1.1.0/lz4-compression-benchmark/)
 - [lz4 decompression](http://jpountz.github.com/lz4-java/1.1.0/lz4-decompression-benchmark/)
 - [net.jpountz.xxhash hashing](http://jpountz.github.com/lz4-java/1.1.0/net.jpountz.xxhash-benchmark/)

# Build

## Requirements

 - JDK version 6 or newer,
 - ant,
 - ivy.

If ivy is not installed yet, ant can take care of it for you, just run
`ant ivy-bootstrap`. The library will be installed under ${user.home}/.ant/lib.

## Instructions

Then run `ant`. It will compile C and Java code and generate a self-contained
JAR file under the dist directory.

