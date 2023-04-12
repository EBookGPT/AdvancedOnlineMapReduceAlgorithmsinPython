# Chapter 3: Basic Map-Reduce Algorithms in Python

Greetings dear reader, and welcome to our third chapter on Advanced Online Map-Reduce Algorithms in Python. In the previous chapter, we covered some advanced Python programming techniques, which will come in handy when we start implementing our map-reduce algorithms.

This chapter will focus on the basic map-reduce algorithms in Python. Map-reduce is a programming model and technique for processing large data sets with a parallel and distributed algorithm on a cluster of computers. The model comprises of two main operations, namely Map and Reduce. 

The Map operation applies a function to every element in the collection and produces a new collection. The Reduce operation then gathers and combines the elements of the new collection into a single value. The idea is to divide the input dataset into smaller chunks, apply the Map operation independently on each chunk, and then apply the Reduce operation on the intermediate results obtained from the Map operation.

We shall start by implementing the basic version of a Map-Reduce algorithm in Python. The aim will be to count the number of occurrences of each word in a given text. Next, we will discuss how to implement parallel map-reduce on a cluster of computers.

So, buckle up, grab a cup of coffee, and let's start diving into the world of Map-Reduce in Python!
# Chapter 3: Basic Map-Reduce Algorithms in Python

## The Mystery of the Missing Documents

Sherlock Holmes, the legendary detective, was presented with a curious case by a client, who worked as a librarian in one of the most reputed libraries in London.

The client informed Sherlock that several important documents had gone missing from the library's archives, which contained valuable information about the history of London. The librarian, along with his team, had searched high and low and questioned every employee, but to no avail. 

Sherlock was intrigued by this case and decided to take it on. The library's archives contained petabytes of data, which made it impossible to search for every document manually. So, Sherlock decided to employ a Map-Reduce algorithm to find out which documents had been removed from the archives.

## The Solution

Sherlock started by implementing the basic version of a Map-Reduce algorithm in Python, which aimed to count the number of occurrences of each word in the archive's documents. The idea was to identify the most frequently occurring words, which would give Sherlock an idea of which documents were most likely to contain valuable information.

```python
def map(document):
    word_counts = {}
    for word in document.split():
        if word in word_counts:
            word_counts[word] += 1
        else:
            word_counts[word] = 1
    return word_counts

def reduce(word_counts):
    total_word_counts = {}
    for word, count in word_counts.items():
        if word in total_word_counts:
            total_word_counts[word] += count
        else:
            total_word_counts[word] = count
    return total_word_counts
```

Sherlock then implemented parallel map-reduce on a cluster of computers, which sped up the process of identifying the most frequently occurring words. Once Sherlock had a list of documents that contained these words, he was able to narrow down his search to those documents and eventually found the missing documents hidden away in a false storage area in the library's archives.

Thanks to the power of Map-Reduce in Python, Sherlock was able to efficiently search through petabytes of data and solve the case. And with that, Sherlock returned the missing documents to the librarian, and justice was served.

## Conclusion

As we saw in our mystery, Map-Reduce in Python can be a powerful tool for processing large amounts of data and solving complex problems. By dividing the input dataset into smaller chunks and applying the Map and Reduce operations, we can efficiently search for important information and obtain faster results. In the next chapter, we'll delve deeper into more advanced Map-Reduce algorithms and techniques in Python.
# Chapter 3: Basic Map-Reduce Algorithms in Python

## Explaining the Map-Reduce Algorithm Used in the Solution

In the Sherlock Holmes mystery, we saw how a Map-Reduce algorithm implemented in Python helped Sherlock efficiently search through petabytes of data and solve a complex case involving missing documents.

Let's take a closer look at the code used to implement this Map-Reduce algorithm.

```python
def map(document):
    word_counts = {}
    for word in document.split():
        if word in word_counts:
            word_counts[word] += 1
        else:
            word_counts[word] = 1
    return word_counts

def reduce(word_counts):
    total_word_counts = {}
    for word, count in word_counts.items():
        if word in total_word_counts:
            total_word_counts[word] += count
        else:
            total_word_counts[word] = count
    return total_word_counts
```

Here, we have two functions: `map` and `reduce`. The `map` function takes in a document and counts the number of occurrences of each word in the document using a dictionary. The output is a dictionary consisting of each word in the document and its corresponding count. This function is applied independently to each document in the input dataset.

The `reduce` function takes in the dictionaries outputted by the `map` function and combines them into a single dictionary with the total count for each word.

Finally, we can apply this Map-Reduce algorithm on a cluster of computers in parallel to obtain faster results.

```python
from multiprocessing import Pool

def parallel_map_reduce(documents):
    p = Pool(4)
    word_counts = p.map(map, documents)
    total_word_counts = reduce(word_counts)
    return total_word_counts
```

In this code, we use the `multiprocessing.Pool` class to create a pool of processes that can work in parallel. We then use the `map` function of this pool to apply the `map` function to each document in the input dataset. We then combine the results using the `reduce` function and return the total word count dictionary.

And that's how Map-Reduce in Python helped Sherlock solve his case!