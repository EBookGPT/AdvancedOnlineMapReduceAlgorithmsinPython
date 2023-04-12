# Chapter 5: Developing Applications using Map-Reduce Design Patterns

Welcome back! In the previous chapter, we delved into advanced Map-Reduce algorithms in Python. Now, it's time to take our learning further and see how to develop applications using Map-Reduce design patterns.

As you may recall, Map-Reduce is a popular programming model used to process large amounts of data over clusters of computers. In order to efficiently process data, it's important to choose the right design pattern that fits your application's needs.

In this chapter, we'll explore various Map-Reduce design patterns and understand their use cases. We'll also see how Python can be used to implement these patterns and how we can execute them on a Hadoop cluster.

So, let's put on our thinking caps, grab our virtual swords, and get ready to apply our Map-Reduce skills to build applications that even Robin Hood would be proud of!
# Chapter 5: Developing Applications using Map-Reduce Design Patterns

## The Tale of Robin Hood and the Unruly Tax Collectors

Robin Hood and his Merry Men were all set to celebrate yet another successful ambush on the tax collectors of Nottingham. However, their celebration was cut short when their scout reported that a large shipment of taxes was set to arrive in the town the next day.

Worried that their previous tactics wouldn't be enough to tackle the large shipment, Robin Hood put on his thinking cap and decided to apply his knowledge of Map-Reduce design patterns to the problem.

After analyzing the situation, Robin Hood decided that the "Counting with Counters" design pattern would be the ideal solution. This pattern allows one to keep a count of specific metrics during Map-Reduce tasks, which could be useful to analyze the shipment's size, distribution, and other factors.

Robin Hood quickly got to work and set up a Python script that utilized the Map-Reduce job tracker to implement the Counters design pattern. The script processed the tax data in chunks, counted relevant metrics, and stored the results using Hadoop's DistributedCache.

The results were eye-opening. Robin Hood realized that the taxes were being distributed in an uneven manner, with certain areas of the town receiving a huge amount of taxes while others hardly got any. This discovery led Robin Hood to develop a new strategy for attacking the shipment, one that would target the areas with the highest concentration of taxes.

The next day, as the tax shipment arrived, Robin Hood and his men sprang into action with their new strategy. Thanks to the insights uncovered by their Map-Reduce application, they were able to ambush the tax collectors in a much more efficient manner, not only collecting their usual take but also uncovering a hidden stash of gold.

And so, Robin Hood and his men celebrated yet another successful ambush. But this time, they knew that it was their knowledge of advanced Map-Reduce algorithms and design patterns that had made all the difference.

## The Resolution

As we saw in the tale of Robin Hood, Map-Reduce design patterns can be extremely useful in developing applications that process large amounts of data. The Counters design pattern showed us how keeping track of metrics during Map-Reduce tasks can help us analyze data and uncover valuable insights.

In this chapter, we explored several Map-Reduce design patterns and their use cases. We also saw how Python can be used to implement these patterns and execute them on a Hadoop cluster.

By applying these design patterns and utilizing our Map-Reduce skills, we can build applications that can solve even the most challenging data processing problems. So, let's keep learning and keep innovating with Map-Reduce!
# Chapter 5: Developing Applications using Map-Reduce Design Patterns

## The Code Behind the Story

In the tale of Robin Hood and the Unruly Tax Collectors, we saw how Robin Hood was able to successfully ambush the tax collectors by utilizing the Counters design pattern with Map-Reduce. Let's take a closer look at the code behind the story.

### The Mapper Function

```python
def mapper(key, value):
    # Parsing the input data
    data = value.strip().split('\t')
    location = data[0]
    taxes = float(data[1])

    # Emitting counter values
    yield location, taxes
    yield "total_taxes", taxes
```

The mapper function receives the input data, which consists of a location and the taxes collected at that location. The function then emits two sets of key-value pairs:
- One pair consisting of the location and the taxes collected at that location.
- Another pair consisting of the string "total_taxes" and the taxes collected at that location.

The idea behind emitting these counters is to keep track of the taxes collected at each location and the overall taxes collected across all locations.

### The Reducer Function

```python
def reducer(key, values):
    if key == "total_taxes":
        # Calculating the sum of all collected taxes
        total_taxes = sum(values)
        # Setting the counter value
        HadoopJobRunner.set_counter("total_taxes", total_taxes)
    else:
        # Calculating the average taxes collected at the location
        avg_taxes = sum(values) / len(values)
        # Emitting the location and average taxes collected
        yield key, avg_taxes
```

The reducer function receives the key-value pairs emitted by the mapper function. If the key is "total_taxes", the function calculates the sum of all collected taxes and sets the counter value of "total_taxes" using Hadoop's set_counter function.

If the key is a location, the function calculates the average taxes collected at that location by summing up all the taxes collected and dividing it by the total number of values received. It then emits the location and the calculated average taxes collected.

### The Driver Function

```python
if __name__ == '__main__':
    # Configuring the job using HadoopJobRunner
    with HadoopJobRunner(input_path='taxes/*', output_path='results', num_reducers=3) as runner:
        runner.run(mapper, reducer)
    # Retrieving the counter value
    total_taxes = HadoopJobRunner.get_counter("total_taxes")
    print("Total taxes collected: ", total_taxes)
```

The driver function is responsible for configuring the Map-Reduce job and executing it using HadoopJobRunner. In this case, we set the input path to 'taxes/*' to read all the tax data files, set the output path to 'results' to store the calculated results, and set the number of reducers to 3.

After the job has run successfully, we retrieve the counter value using HadoopJobRunner's get_counter function and print it to the console.

### Conclusion

This example shows how we can implement the Counters design pattern using Map-Reduce in Python. The code processes the tax data, keeps track of the taxes collected at each location, and calculates the overall taxes collected across all locations. The insights gathered using the Counters design pattern allowed Robin Hood to plan a better ambush and ultimately uncover a hidden stash of gold.