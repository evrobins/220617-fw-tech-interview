# Answer to checksums question
## Everett Robinson

> What are checksums and what are they useful for?

Checksums have many uses in the computing world. They are usually used to detect changes and/or errors in a block of information, e.g. a packet or a file. Checksums are the result of a mathematical operation on that information.

A checksum used for detection of a single bit error commonly uses the XOR (exclusive-or) operation. A common checksum for packets uses both the XOR and the addition operations (hence the name "checksum"), which is likely to catch errors in two bits or more.

Checksums are also used to validate that data has not been changed from its original source. For this purpose, a "one-way" operation is used, that is one that is difficult to reverse. The common operation is called a "hash", which divides the data into fixed-length pieces and then passes them through a large polynomial function. That makes it difficult for a third party to change part of the data block while attaining the same checksum.