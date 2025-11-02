# MinHash LSH in Milvus: The Secret Weapon for Fighting Duplicates in LLM Training Data

May 16, 2025 Li Liu, Yaya Cheng

*Large Language Models* (LLMs) have transformed the AI landscape with their ability to write code, create content, and solve complex problems.
However, these powerful models require enormous amounts of high-quality data to fuel their training.

The challenge is that raw training data often contains significant redundancy.
It’s like teaching a child by repeating the same lessons over and over while skipping other important topics.
A large AI company approached us with precisely this problem - they were building an ambitious new language model but struggled with deduplicating tens of billions of documents.
Traditional matching methods couldn’t scale to this volume, and specialized deduplication tools required massive computational resources, making them economically unviable.

To solve this problem, we introduced *MinHash* LSH (*Locality Sensitive Hashing*) indexing in Milvus 2.6.

[This article](https://milvus.io/blog/minhash-lsh-in-milvus-the-secret-weapon-for-fighting-duplicates-in-llm-training-data.md)
explores how MinHash LSH efficiently solves the data deduplication problem for LLM training.

*MinHash* (or the min-wise independent permutations locality sensitive hashing scheme) is a technique for quickly estimating how similar two sets are.
The scheme was published by Andrei Broder in a 1997 conference, and initially used in the AltaVista search engine to detect duplicate web pages and eliminate them from search results.
It has also been applied in large-scale clustering problems, such as clustering documents by the similarity of their sets of words.

[1] [Andrei Broder (1998) "On the resemblance and containment of documents"](positano-final-wpnums-1998.pdf)

[Rensa: MinHash in Rust](https://github.com/beowolx/rensa)
