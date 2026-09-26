# *QUICK START GUIDE*


The Stateshaper Engine will give you a list/array of deterministic numbers to tokenize for use to call events or define variables in your logic. 

For continuous use, the engine can be called in a loop using the *run_engine* function. For one time, call it once with a specific *token_count* parameter.

To create the same output again, *start_engine* needs to be called once more.

<br> <br>

<h3><b><u>Steps<br>
--------
</b></h3> 


1\. Make sure your data is in one of the formats listed in the *"example_data"* directory. If needed, use the *FormatData* class in the nested *'format_data'* directory.

Instructions: [`Formatting Data for Input`](example_data/format_data/FORMAT_DATA.md)

<br> 

2\. Initialize a *RunEngine* class 

```python
# data (REQUIRED) - Te input data. Must be in a format listed in the 'example_data' directory
# seed (optional) - Masked values used to decode preferred attributes for the 'ratings' ruleset. (ex. seed={"v": ["ABC12345", "BVCH457SZ"]})
# token_count (default=10) - The desired size of the list containing your input terms.
# initial_state (default=[66, 67, 54, 3, 34]) - The original starting values to base the chain on. These can be custom if a different output sequence is desired. The same initial state is required to re-create the same output. A single integer can also be passed instead of an array.
# constants (optional) - Only change this for custom morphing equations.
# mod (optional) - Only change this for custom morphing equations.

from stateshaper import RunEngine 

#BASIC (first run)
engine = RunEngine(data=your_data, token_count=needed_tokens)

# RE-CREATE PREVIOUS OUTPUT
engine = RunEngine(data=your_data, seed=created_seed, token_count=needed_tokens)

#CUSTOM
engine = RunEngine(data=your_data, seed=created_seed, token_count=needed_tokens, initial_state=optional_custom_logic, constants=optional_custom_logic, mod=more_optional_logic)

engine.start_engine()

# TO GET NEEDED VALUES TO RE-CREATE THE SAME OUTPUT
# Not needed if no custom values were originally passed. 
engine.get_seed()

# With compressed vocab
engine.get_seed(vocab=True)
```

**IMPORTANT!**
***To create determinism, the initial state, constants and mod value are required each time the engine starts. Only the initial state is needed if no other custom values were passed to generate the ouput.***

<br>

3\. Call the *run_engine* method.

```python
engine.run_engine()

# OUTPUT    
#
# ["your", "input", "values", "are", "returned", "based", "on", "chosen", "stateshaper", "rules"]
```

<br>

4\. OPTIONAL Call the *rebuild* method or re-instantiate the class to start from the beginning.

```python
engine.rebuild()

# OR

engine = RunEngine(data=your_data, seed=create_seed, token_count=needed_tokens)
```


Whatever the decided use is, this tool can achieve it using almost no stored memory. 

Unlimited sequences of data can be re-created from a small seed, including fully personalized user profiles. 

Privacy is achieved through obfuscation. The data can't be interpreted without using the seed as a key.
