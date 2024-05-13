# cppsimhash

C++ simhash implementation for documents
and an additional (prototype) simhash index for text documents.

Simhash is a hashing technique that belongs to the LSH (Local Sensitive Hashing) algorithmic family.
It was initially developed by Moses S. Charikar in 2002 and is described in detail in his [paper](http://www.cs.princeton.edu/courses/archive/spring04/cos598B/bib/CharikarEstim.pdf).
The main goal of this algorithm is to detect near duplicate documents, since similar documents will most probably 
have similar (or even the same) simhash value. 
A straightforward explanation of the Simhash algorithm can be found [here](http://matpalm.com/resemblance/simhash/).

### How it works

The unique and most interesting characteristic of the Simhash algorithm is that near duplicate documents will most likely 
have the same (or pretty similar) hash value. This feature makes it very useful when it comes to near duplicate document detection 
since it doesn’t require to compare all the documents with each other. That comparison would result to a $O(n^2)$ complexity.
By using simhash we no longer need a pair-wise comparison between all the documents. We only need a single pass over our collection. 
After calculating the hash values for all the documents we just need to compare the ones that share the same (or similar) hash values which results in an $O(n)$ complexity.

More specifically, in order to calculate the simhash value of a document we perform the following steps:

1. Split the document in tokens (words, characters or n-grams)
2. Hash each token separately using MD5
3. Calculate the bit representation of this MD5 hashes
4. Calculate and apply a weight to each of the document’s tokens. For example, these weights are the term frequencies in the document.
5. Merge the bit representations of all the tokens of the document in order to calculate the document’s final hash value.


# Required

* python3
* scons
* g++ (c++14)
* cpu with hardware aes, `cat /proc/cpuinfo | grep "aes" | wc -l` should be > 0


# Build Steps

Just run `scons`


# Simidx -- usage

add a text document using `simidx.py`:
```
# add one document
./simidx.py add textfile

# add a folder
./simidx.py add textfolder

# after you created an index you can query it with
./simidx.py query <document.txt>
```

# Idea

For the approach and core idea have a look at papers in `doc`.

