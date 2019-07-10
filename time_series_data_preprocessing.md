I have come into a lot of problems while I read a paper "deep knowledge tracing". This paper use a dataset called "assistment". It looks like this:
```
"builder_train.csv"
1
7,
1,
7
82,82,82,82,82,82,82,
0,0,0,0,0,0,0,
```
The first line means that the following time series contains '1' time step. The second line is question id and the third line is whether the answer is correct corresponding to the question. So the '7' and '1' means that a student did exercise7 and did it right. The fourth line '7' means the following time series will contain seven time step.

At first, I plan to scan through the data and get a non-repeatable dict of question id. 
```
def add_to_dict():
    #将未出现的exercise的序号加入字典
    for num in quest_id_list:
        if num not in dict_skill:
            dict_skill[num] += 1

while row != []:
    row = next(train_file)
    quest_id_list = [int(x) for x in row if x!='']
    add_to_dict()
    row = next(train_file)
    row = next(train_file)

with open(skill_output,'a+') as file_output:
    for skill,cnt in dict_skill:
        file_output.write(skill+'\n')
```
But I run into Iterable error: "Exception has occurred: StopIteration". I had limited the while loop to limited times like 5 and 100, which all went ok. But when I run the code on the whole data, it went wrong.

So I start to think if I can scan first 300 lines of data, and write the dict to the file and initialize the dict and counter to avoid the error. But then another problem arises -- how could I know that there will not be repeated question id in multiple dict I write to the file?