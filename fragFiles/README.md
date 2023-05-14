# Fragment files

This folder contains the starting "substrates" for the insulin gene assembly challenge. Each file contains the insulin gene that I have fragments (sonicated) in some way.


## During the workshop (students please read!)

If you are currently in class participating in the workshop you only need to worry about a couple files.

To get started testing your assembly algorithim I recommend using the `TESTING_fragmentsLevel0.txt` file.
This file is just like the real deal but only contains a very small number of fragments and you can check
your answer by looking at the sequence in `TESTING_ANSWER_fragmentsLevel0.txt`.

You can use the Python function below to read the test fragments and the answer file. The function will
return a tuple. The first item is the correct answer as a string and the second is a list of the 
test fragments.

```Python
def download_test_data():
    import requests
    """Downloads level 0 test data and correct answer. Returns a tuple. First value is the correct
    answer as a string and second are the test fragments as a list of strings.
    """
    import requests
    frags = requests.get(
        'https://raw.githubusercontent.com/EthanHolleman/RCWorkshop/main/fragFiles/TESTING_fragmentsLevel0.txt'
    
    )
    frags = frags.text.split('\n')[:-1] 
    
    answer = requests.get(
        'https://raw.githubusercontent.com/EthanHolleman/RCWorkshop/main/fragFiles/TESTING_ANSWER_fragmentsLevel0.txt'
    )
    answer = answer.text.strip()
    
    return answer, frags
```

## Reading the real gene fragments file

All fragment files contain one fragment per line. Thats it. For the sake of time there is a function below
that you can copy and paste to download the level 0 fragments and return them as a list of strings.

```python
def download_frags():
    """Downloads level 0 fragments for insulin assembly challenge from GitHub and
    returns them as a list of strings.
    """
    import requests
    response = requests.get(
        'https://raw.githubusercontent.com/EthanHolleman/RCWorkshop/main/fragFiles/fragmentsLevel0.txt'
    
    )
    return response.text.split('\n')[:-1]  # there is extra \n at end of file
```

## How were these files generated?

### `fragmentsLevel0.txt`

The insulin gene was broken into 20 character (nucleotide) fragments so that each fragment overlaps
by 5 characters with the previous fragment so you end up with an overlap pattern that should
look something like the example below.

```
FRAGMENT1
      FRAGMENT2
            FRAGMENT3
                 FRAGMENT4
```

### `fragmentsLevel1.txt`

Here instead of fragmenting the insulin gene as uniform chunks I produced fragments that
are much more realistic to what you might get from actual shotgun sequencing data. This
was done by generating a random start position within the insulin gene and a random
fragment length. The sequence of the gene from the start position to the start position
plus the length was then returned as the fragment sequence. This was repeated 5000
times to produce the final `fragmentsLevel1.txt`.

This means that a fragment may overlap with many or no other fragments. The overlap
might not be on the ends of the fragment. There may be fragments that are duplicates
or close to duplicates. 

This is a much better simulation of what trying to assemble shotgun sequncing data
would be like and is a serious problem. The jump in difficulty from level 0 to level
1 is signifcant. 


### `fragmentsLevel2.txt`

The final boss. The level 2 file was generated the same way as the level 1 file but I have
introduced a 5% error rate at each character. That means that for each character (nucleotide)
in the fragment there is a 5% chance I changed to to a different nucleotide (A, T, G or C).

Good luck!
