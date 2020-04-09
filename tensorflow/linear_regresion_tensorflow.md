## Tensorflow Implementation and Mathematics for Linear Regression

### Mathematics

$$F(x) = \int^a_b \frac{1}{3}x^3$$

### Implementation
* Initializing all variables and getting data ready
  ```python
  LR = 0.01
  EPOCHES = 300

  NUMBER_OF_SAMPLE = 500
  X_train = np.linspace(0,100, NUMBER_OF_SAMPLE)
  Y_train = 4*X + 12*np.random.randn(NUMBER_OF_SAMPLE)
  ```
* Creating Computational Graph
  ```python
  x = tf.placeholder(tf.float32)
  y = tf.placeholder(tf.float32)

  w = tf.Variable(np.random.randn(), name="weight")
  b = tf.Variable(np.random.randn(), name='bias")

  pred = tf.add(tf.maltiply(w,x), b)
  cost = tf.div(tf.reduced_sum(tf.pow(tf.sub(pred,y),2)),2*NUMBER_OF_SAMPLE) 
  ```
* Define Computation Parameters and Compute
  ```python
  optimizer = tf.optimizers.GradientDescentOptimizer(LR).minimize(cost)
  init = tf.global_variable_initializer()

  with tf.Session() as sess():
    sess.run(init)
    for epoch in range(EPOCHES):
      for X,Y in zip(X_train,Y_train):
        sess.run(optimizer, feed_dict={x:X, y:Y})
      if not epoch%10:
        w1 = sess.run(w)
        b1 = sess.run(b)
        cost1 = sess.run(cost, feed_dict={x:X, y:Y})
        print(w1, b1, cost1)
  ```