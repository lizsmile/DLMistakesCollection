## optimizer
https://blog.csdn.net/hustqb/article/details/80302726
optimizer.minimizer() concludes two steps:
    1. calculate gradient
    2. apply gradient to update parameters
so in application, if we want to look into the training process, we can get all gradient value from```trainable_variables```
and break minimizer into:
    1. ```optimizer.compute_gradients()```to calculate gradient
    2. do anything you like to gradient, like clip or add noise
    3. ```optimizer.apply_gradients()```to update gradient

## tf.summary
### tf.summary.histogram
https://tensorflow.google.cn/api_docs/python/tf/summary/histogram?hl=en

### tf.nn.zero_fraction()
Tensorflow-tf.nn.zero_fraction()的作用是将输入的Tensor中0元素在所有元素中所占的比例计算并返回，因为relu激活函数有时会大面积的将输入参数设为0，所以此函数可以有效衡量relu激活函数的有效性。

```
student_id = 0
with open(skill_output,'a+') as file_output:
    while True:
        nStepsStr = next(train_file)
        questionIdStr = next(train_file)
        correctStr = next(train_file)
        if nStepsStr == [] or questionIdStr == [] or correctStr == []:
            break
        nStepsStr = int(nStepsStr[0])
        questionIdStr = [x for x in questionIdStr if x!='']
        correctStr = [y for y in correctStr if y!='']
        for i in range(nStepsStr):
            file_output.write(str(student_id)+' '+questionIdStr[i]+' '+correctStr[i]+'\n')

        student_id += 1

file_output.close()
```
In the above code, there will always be error. I guess it is because I didn't use next right. When ```next```is used in infinite loop, it will cause an error. 
https://blog.csdn.net/lwbeyond/article/details/60959727
So I refered the above link, and made some changes to the code.
After several tests, I finally get a not bad result. the code above can actually work but at the last loop, when the reader get an empty line, an error triggers. So we just need to ignore it!