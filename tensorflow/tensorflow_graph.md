## Understanding Tensorflow and Tensorboard

### Tensor:
* Container
* Use to store n dimentional Data

### Tensorflow:
* Tensor+flow
* Functions as computational Graphs and execute them using sessions.
* Two step process: building a graph and running that graph
* Building is a simple and straight forward process just take create the variables using tensorflow's Tensor container, Apply operations using tensorflow's in built  operations like tf.add(), tf.matmul(), etc.
* After that process graph will be created, one one thing to note that the computation has not been done yet means, if you print the output of y, you will get nothing.
  ```python
  a = tf.constant(3)
  b = tf.constant(12)
  c = tf.add(a, b)
  ```
* In order to compute the results you need to run it inside a session, A session is not but a process name in which computational graph is loaded into the ram and data flow through it compute the final results
  ```python
  with tf.Session() as sess:
    out = sess.run(c) #c is the computation that you want to run
    print(out)
  ```

### TensorBoard
* TensorBoard is a visualization suite for visualizing tensorflow graph and data.
* How to Create tensorflow event file, tensorflow event file will log details about the tensorflow session
  ```python
  with tf.Session() as sess:
    writer = tf.summary.FileWriter('./logs', sess.graph)
    out = sess.run(c)
    writer.close()
  ```
* ***tf.name_scope():*** A context manager for use when defining a Python op. It is help in reducing the messy ness of computational graph by clustering them into collapsable clusters.
  ```python
  with tf.name_scope("Graph"):
    a = tf.constant(3)
    b = tf.constant(12)
    with tf.name_scope("Scope_1"): 
      c = tf.add(a, b)
  ```
* ***tf.summary.scalar:*** Keep track of variable change during computation using this function. generally used for logging values like variable change, losses, acurracy,etc.
  ```python
  ...
  some_variable = tf.get_variable()
  summary_variable = tf.summary.scalar("name", tensor = some_variable)
  init = tf.global_variable_initializer()
  with tf.Session() as sess:
    writer = tf.summary.FileWriter('./log', sess.graph)
    for counter in range(something)
      sess.run(init)
      value_of_variable = sess.run(summary_variable)
      writer.add_summary(value_of_variable, counter) # log changes in varibale
  ```
  The changes in variable value can be visulialize in tensorboard as line plot
* ***tf.summary.histogram:*** Used for non scalar tensor, generally used to visualize changes in weight ans bias
  ```python
  ...
  weight = tf.get_variable('weight_1', shape=[100,100], initialization='normal')
  weight_summary = tf.summary.histogram('name', tensor=weight)
  ...
    ...
      summary_2 = sess.run(weight_summary)
      writer.add_summary(summary_2, counter)
  ```
